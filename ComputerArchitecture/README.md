# Computer Network
## Client
```c

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>
#include <sys/socket.h>

#define BUF_SIZE 1024
void error_handling(char *message);

int main(int argc, char *argv[])
{
	int sd;
	FILE *fp;
	
	char file_name[BUF_SIZE];
	char buf[BUF_SIZE];
	int read_cnt;
	int read_size = 0;
	struct sockaddr_in serv_adr;
	if (argc != 4) {
		printf("Usage: %s <IP> <port> <file name> \n", argv[0]);
		exit(1);
	}

	strcpy(file_name, argv[3]);
    int len = strlen(file_name);

	fp = fopen(argv[3], "rb");
    if(fp == NULL){
        printf("failed to read file\n");
    }
	sd = socket(PF_INET, SOCK_STREAM, 0);   

	memset(&serv_adr, 0, sizeof(serv_adr));
	serv_adr.sin_family = AF_INET;
	serv_adr.sin_addr.s_addr = inet_addr(argv[1]);
	serv_adr.sin_port = htons(atoi(argv[2]));

	connect(sd, (struct sockaddr*)&serv_adr, sizeof(serv_adr));
    printf("connect successed!\n");
	
	// TODO: Send file name to server 
    write(sd, &len, sizeof(len));
    write(sd, file_name, strlen(file_name) + 1);

	// TODO: Send file data (Hint: file_server.c)

    while(1)
	{   
        read_cnt = fread(buf, 1, BUF_SIZE, fp);

        buf[read_cnt] = '\0';
        read_size += read_cnt;
		
		if (read_cnt < BUF_SIZE)
		{   
			write(sd, buf, strlen(buf) + 1);
			break;
		}

		write(sd, buf, BUF_SIZE);
	}

	// TODO: read complete message from server
	memset(buf, 0, sizeof(buf));
    
    printf("Result from Server\n");
	while((read_cnt = read(sd, buf, BUF_SIZE)) != 0){
        if(read_cnt < BUF_SIZE){
            printf("%s", buf);
            break;
        }
        printf("%s", buf);
    }
	printf("\n\n");
	fclose(fp);
	close(sd);
	return 0;
}

void error_handling(char *message)
{
	fputs(message, stderr);
	fputc('\n', stderr);
	exit(1);
}
```
## Server
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>
#include <sys/socket.h>
#include <pthread.h>

#define FILE_LEN 32
#define BUF_SIZE 1024
void error_handling(char *message);
void *handle_client(void *arg);
pthread_mutex_t mutex;

struct client_info  //thread에 argument로 전달하기 위한 구조체
{
    int client_socket;
    struct sockaddr_in client_addr;
};

int main(int argc, char *argv[])
{
    int serv_sd, clnt_sd;  //server socket 파일 디스크립터, client socket 파일 디스크립터
    pthread_t thread;  //쓰레드 변수

    struct sockaddr_in serv_adr, clnt_adr;  //server 주소를 담을 구조체, client 주소를 담을 구조체
    socklen_t clnt_adr_sz;  //각 주소에 대한 구조체의 size

    if (argc != 2)
    {
        printf("Usage: %s <port>\n", argv[0]);
        exit(1);
    }

    serv_sd = socket(PF_INET, SOCK_STREAM, 0);

    memset(&serv_adr, 0, sizeof(serv_adr));
    serv_adr.sin_family = AF_INET;
    serv_adr.sin_addr.s_addr = htonl(INADDR_ANY);
    serv_adr.sin_port = htons(atoi(argv[1]));

    if (bind(serv_sd, (struct sockaddr *)&serv_adr, sizeof(serv_adr)) == -1)
        error_handling("bind() error");
    if (listen(serv_sd, 5) == -1)
        error_handling("listen() error");

    while (1)
    {
        clnt_adr_sz = sizeof(clnt_adr);
        clnt_sd = accept(serv_sd, (struct sockaddr *)&clnt_adr, &clnt_adr_sz);

        struct client_info clnt_info;
        clnt_info.client_socket = clnt_sd;
        clnt_info.client_addr = clnt_adr;

        // TODO: pthread_create & detach
        pthread_create(&thread, NULL, (void *)handle_client, &clnt_info);  //쓰레드 생성
        pthread_detach(thread);  //쓰레드 detach -> 독립적인 쓰레드 실행
    }

    close(serv_sd);
    return 0;
}

void *handle_client(void *arg)
{
    // TODO: file receiving
    struct client_info clnt_info = *((struct client_info *)arg);
    FILE *fp;
    int read_cnt, read_size;
    char buf[BUF_SIZE];  //BUFFER의 사이즈가 client와 같아야 한다.
    char filename[30];
    char command[512];
    int sock = clnt_info.client_socket;
    struct sockaddr_in clnt_adr = clnt_info.client_addr;
    int len;

    memset(buf, 0, sizeof(buf));
    read_size = 0;

    read(sock, &len, sizeof(len));  //파일 이름의 길이를 먼저 받음
    read(sock, buf, len + 1);  // 파일 이름 + '\0'까지만 입력 버퍼의 내용을 읽음
    strcpy(filename, buf);

    fp = fopen(filename, "w");
    while ((read_cnt = read(sock, buf, BUF_SIZE)) != 0)
    {
        read_size += read_cnt;
        if (read_cnt < BUF_SIZE)
        {
            buf[read_cnt] = '\0';
            fwrite(buf, sizeof(char), strlen(buf), fp);
            break;
        }
        fwrite(buf, sizeof(char), read_cnt, fp);
    }
    fclose(fp);

    printf("Received %s from %s\n", filename, inet_ntoa(clnt_adr.sin_addr));
    printf("Compile %s and return results\n", filename);

    pthread_mutex_lock(&mutex);  //같은 이름의 파일을 실행시키기 때문에 여러 쓰레드가 동시에 실행될 때 일어날 충돌을 방지
    snprintf(command, sizeof(command), "gcc %s -o output && ./output", filename);
    fp = popen(command, "r");
    if (fp == NULL)
    {
        perror("popen() error");
        return NULL;
    }

   while(1)
	{   
        read_cnt = fread(buf, 1, BUF_SIZE, fp);  //fgets로 하면 왜 안됐을까?

        buf[read_cnt] = '\0';
        read_size += read_cnt;
		
		if (read_cnt < BUF_SIZE)
		{   
			printf("%s", buf);
			write(sock, buf, strlen(buf) + 1);
			break;
		}
		printf("%s", buf);
		write(sock, buf, BUF_SIZE);
	}

    pclose(fp);
    pthread_mutex_unlock(&mutex);

    printf("\n------------------------------------\n");
    close(sock);
    return NULL;
}

void error_handling(char *message)
{
    fputs(message, stderr);
    fputc('\n', stderr);
    exit(1);
}
```
client와 server의 소켓 프로그래밍을 할 때 가장 주의 해야 할 점으로 첫번째는 **write을 한 횟수만큼 read가 실행되지 않는다는 것이다.** 실제로 동작하는 것을 보면 ```write```을 한번 하든 두번 하든 ```read```동작이 일어나기 전까지 수신하는 측의 입력 버퍼는 계속해서 채워진다. 그리고 ```read```는 입력 버퍼에 채워진 것을 읽으라고 명령받은 만큼 읽어온다. 즉, ```read(sock, buf, BUF_SIZE)```의 경우 입력 버퍼에 들어온 데이터를 최대 ```BUF_SIZE```만큼 읽는 것이다. 만약 송신하는 측이 길이가 20인 데이터와 30인 데이터를 보냈고 수신받는 측의 한번에 읽는 데이터 크기가 80이라면 두번에 걸쳐서 보냈어도 ```read```동작이 실행되기 전에 입력 버퍼에 들어온다면 한번에 다 읽어 들이게 된다. 그렇기 때문에 보내고 싶은 데이터가 한 가지가 아니라면 **Data size를 먼저 보내서 해당 길이만큼만 버퍼에서 읽어오는 동작이 필요하다.** 
<br><br>두 번째로 조심해야 할 것은 송신하는 측에서 한번에 ```write```하는 데이터 크기와 수신하는 측에서 ```read```하는 크기가 다를 경우이다. 송신측의 데이터 사이즈가 더 크다면 상관이 없지만 더 작다면 문제가 생긴다. 만약 ```read``` 함수의 반환값이 최대로 읽을 수 있는 크기보다 더 작은 경우에 송신이 끝났다고 판단하고 더 이상 버퍼를 읽는 동작을 멈추는 방식으로 반복문을 작성했다면, ```write```가 아직 다 보내지 않았지만 ```read```가 동작하여 최대로 읽을 수 있는 크기보다 더 작은 수를 반환할 수도 있다. 따라서 이 경우 **write를 하는 크기와 read를 하는 크기를 같게 함으로써 해결할 수 있다.**
