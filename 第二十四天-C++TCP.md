# 第二十四天 C++ 實作 TCP Server

在這個段落，我會跟著參考資料的 YoutTube 影片用 C++來實作一個[TCP Server](https://zh.wikipedia.org/zh-tw/%E4%BC%A0%E8%BE%93%E6%8E%A7%E5%88%B6%E5%8D%8F%E8%AE%AE)，那就馬不停蹄的開始吧~

## C++ Implementation on TCP Server

1. 首先用 Visula Studio 2022 建立一個空的 C++ 專案，然後在來源檔案的資料夾中新增一個 C++的檔案命名為`main.cpp`

[empty_project]
[main_C++]

2. 然後就在 main.cpp 裡面開始寫程式碼囉

先將一些基本的部分加到`main.cpp`，note: `pragma comment`是用來鏈結外部的 Lib 檔案:

```
#include <iostream>
#include <WS2tcpip.h>

#pragma comment (lib, "ws2_32.lib")

using namespace std;

void main()
{

}
```

3. 使用註解來先宣告要做的事情<-這個是我在一些外國的程式講師發現的用法

個人覺得對寫程式很有用，能夠整理歸納你的程式邏輯，定義出你程式整體流程(flow)，並且能夠再次確認你的程式流程是否符合邏輯

main.cpp

```
void main()
{
	// Initialize winsocket

	// Create a socket

	// Bind the socket to an ip address and port

	// Tell winsocket the socket is for listening

	// Wait for connection

	// Close listening socket

	// While loop: accept amd echo message back to client

	// Close the socket

	// Shutdown winsocket
}
```

4. 接下來就接著各個註解的動作開始實作

main.cpp

```
// Initialize winsocket
WSADATA wsDaata;
WORD ver = MAKEWORD(2, 2);

int wsOk = WSAStartup(ver, &wsDaata);
if (wsOk != 0)
{
    cerr << "Can't Initialize winsocket! Quitting" << endl;
    return;
}

// Create a socket
SOCKET listening = socket(AF_INET, SOCK_STREAM, 0);
if (listening == INVALID_SOCKET)
{
    cerr << "Can't create a socket! Quitting" << endl;
    return;
}

// Bind the ip address and port to a socket
sockaddr_in hint;
hint.sin_family = AF_INET;
hint.sin_port = htons(54000);
hint.sin_addr.S_un.S_addr = INADDR_ANY;// Could also use inet_pton ...

bind(listening, (sockaddr*)&hint, sizeof(hint));

// Tell winsocket the socket is for listening
listen(listening, SOMAXCONN);

// Wait for connection
sockaddr_in client;
int clientSize = sizeof(client);

SOCKET clientSocket = accept(listening, (sockaddr*)&client, &clientSize);

char host[NI_MAXHOST];      // Client's remote name
char service[NI_MAXHOST];   // Service (i.e. port) the client is connect on

ZeroMemory(host, NI_MAXHOST);    // Window version, same as memset(host, 0, NI_MAXHOST);
ZeroMemory(service, NI_MAXHOST);

if (getnameinfo((sockaddr*)&client, sizeof(client),host,NI_MAXHOST, service, NI_MAXHOST,0) == 0)
{
    cout << host << " connected on port " << service << endl;
}
else
{
    inet_ntop(AF_INET, &client.sin_addr, host, NI_MAXHOST);
    cout << host << " connected on port " <<
        ntohs(client.sin_port) << endl;
}

// Close listening socket
closesocket(listening);

// While loop: accept amd echo message back to client
char buf[4096];

while (true)
{
    ZeroMemory(buf, 4096);

    // Wait for client to snd data
    int bytesReceived = recv(clientSocket, buf, 4096, 0);

    if (bytesReceived == SOCKET_ERROR)
    {
        cerr << "Error in recv(). Quitting" << endl;
        break;
    }

    if (bytesReceived == 0)
    {
        cout << "Client disconnected " << endl;
        break;
    }

    // Echo message back to client
    send(clientSocket, buf, bytesReceived + 1, 0);
}

// Close the socket
closesocket(clientSocket);

// Shutdown winsocket
WSACleanup();
```

5. 上面都完成了後，使用`CTRL + B`來建置我們的程式

6. 驗證這個 TCP Server，會使用[Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)來測試

   a. 在 Visual Studio 2022 按`F5`，啟動程式  
   b. 打開 Putty，Host Name 輸入: 127.0.0.1，Port: 54000，`Connection Type: Raw`，因為我們的 TCP 只是最簡單的 protocol，所以其他的類別都不支援  
   [putty]  
   c. 在 Putty 打些內容並按`Enter`送出，可以收到 Server 的回覆
   [demo_putty]

那到此為止，就完整的實作了一個 TCP Server 了~

---

那 30 天重新認識 C++的部分，就先到這邊啦，在剩餘的 6 天我會再介紹剩下幾個主題~

- Quick info OpenCV
- C++ Vector, define, header file
- Design pattern for Singleton, Template, State
- More things in C++ concurrency, parallelism
- Tree algorithm in C++

## 參考資料

[Creating a TCP Server in C++](https://www.youtube.com/watch?v=WDn-htpBlnU&t=937s)  
[What pragma comment actually do](https://stackoverflow.com/questions/12199595/c-what-does-pragma-commentlib-xxx-actually-do-with-xxx)
