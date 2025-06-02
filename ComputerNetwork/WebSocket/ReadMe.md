# Websocket

### 웹소켓이란?
...

**simple_websocket_client.c 전체 코드**
``` c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <netdb.h>
#include <time.h>

#define BUFFER_SIZE 1024

void generate_masking_key(uint8_t mask[]){
    for(int i = 0; i < 4; i++){
        mask[i] = rand() % 256;
    }
};

int main(int argc, char *argv[]){
    int sock;
    struct sockaddr_in serv_addr;

    srand(time(NULL));

    // Check command line arguments.
    if(argc != 4)
    {
        printf("Usage: %s <host> <port> <text>\n"  \
               "Example: \n" \
               "        %s 192.168.10.25 8080 \'Hello, world!\'\n", argv[0], argv[0]); 
        return -1;
    }


    memset(&serv_addr, 0, sizeof(serv_addr));
    serv_addr.sin_family = AF_INET;
    serv_addr.sin_addr.s_addr = inet_addr(argv[1]);
    serv_addr.sin_port = htons(atoi(argv[2]));
    const char* message = argv[3];
    char buffer[BUFFER_SIZE];

    sock = socket(PF_INET, SOCK_STREAM, 0);
    if (sock == -1) {
        perror("socket creation failed");
        exit(EXIT_FAILURE);
    }

    if(connect(sock, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) == -1){
        perror("Connect() error!");
        return -1;
    }

    printf("connect successed");

    const char *ws_con_request = "GET %s HTTP/1.1\r\n"
                    "Host: %s:%d\r\n"
                    "Upgrade: websocket\r\n"
                    "Connection: Upgrade\r\n"
                    "Sec-WebSocket-Key: %s\r\n"
                    "Sec-WebSocket-Version: 13\r\n"
                    "\r\n";
    sprintf(buffer, ws_con_request, argv[1], argv[1], atoi(argv[2]), "erPKMz5t9vwqkJI+RmHnLw==");

    send(sock, buffer, strlen(buffer), 0);
    recv(sock, buffer, BUFFER_SIZE, 0);
    printf("%s", buffer);

    size_t msg_len = strlen(message);
    uint8_t frame[BUFFER_SIZE];
    int frame_index = 0;
    frame[frame_index++] = 0x81;

    if(msg_len < 126){
        frame[frame_index++] = 0x80 | msg_len;
    }
    else if(msg_len < 65536){
        frame[frame_index++] = 0x80 | 126;
        frame[frame_index++] = (msg_len >> 8) & 0xFF;
        frame[frame_index++] = msg_len & 0xFF;
    }
    else{
        printf("message is too long!\n");
    }

    uint8_t mask[4];
    generate_masking_key(mask);

    for(int i = 0; i < 4; i++){
        frame[frame_index++] = mask[i];
    }

    for(int i = 0; i < msg_len; i++){
        frame[frame_index++] = message[i] ^ mask[i%4];
    }

    send(sock, frame, frame_index, 0);

    int recv_len = recv(sock, buffer, BUFFER_SIZE, 0);
    if (recv_len > 0) {
        printf("Received %d bytes: ", recv_len);
        for (int i = 0; i < recv_len; i++) {
            if ((unsigned char)buffer[i] >= 32 && (unsigned char)buffer[i] < 127)
                printf("%c", buffer[i]);
            else
                printf(".");
        }
        printf("\n");
    }

    frame_index = 0;
    frame[frame_index++] = 0x88;
    frame[frame_index++] = 0x82;

    generate_masking_key(mask);
    for (int i = 0; i < 4; i++) {
        frame[frame_index++] = mask[i];
    }


    uint16_t close_code = htons(1000);
    frame[frame_index++] = ((uint8_t *)&close_code)[0] ^ mask[0];
    frame[frame_index++] = ((uint8_t *)&close_code)[1] ^ mask[1];

    send(sock, frame, frame_index, 0);
    recv(sock, buffer, BUFFER_SIZE, 0);

    close(sock);
    return 0;
}

```
