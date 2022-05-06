---
title: C++后端学习——WebServer
date: 2022-04-08 14:31:07
tags: 
  - C++
  - Linux
  - Socket
---

# C++后端学习——WebServer

为找C++实习而进行学习WebServer源码

### 1. handle_for_sigpipe()

处理忽略SIGPIPE信号，防止因为错误的写操作（向读端关闭的socket中写数据）而导致进程退出

```cpp
void handle_for_sigpipe()
{
    struct sigaction sa;
    memset(&sa, '\0', sizeof(sa));//'\0'结束标志
    sa.sa_handler = SIG_IGN;//SIG_IGN表示忽略此信号.
    sa.sa_flags = 0;
    if(sigaction(SIGPIPE, &sa, NULL))
    
        return;
}

```

```cpp
//sigaction 的定义如下：
    /*struct sigaction{
        void (*sa_handler)(int);
        sigset_t sa_mask
    
        int sa_flags;
    
        void (*s_sigaction)(int ,siginfo_t *,void*);
    };*/
    
    //int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);
    //signum参数指出要捕获的信号类型，act参数指定新的信号处理方式，oldact参数输出先前信号的处理方式（如果不为NULL的话）。
```

对一个对端已经关闭的socket调用两次write, 第二次将会生成**SIGPIPE**信号, 该信号默认结束进程.

具体的分析可以结合TCP的"四次握手"关闭. TCP是全双工的信道, 可以看作两条单工信道, TCP连接两端的两个端点各负责一条. 当对端调用close时, 虽然本意是关闭整个两条信道, 但本端只是收到FIN包. 按照TCP协议的语义, 表示对端只是关闭了其所负责的那一条单工信道, 仍然可以继续接收数据. 也就是说, 因为TCP协议的限制, 一个端点无法获知对端的socket是调用了close还是shutdown.

对一个已经收到FIN包的socket调用read方法, 如果接收缓冲已空, 则返回0, 这就是常说的表示连接关闭. 但第一次对其调用write方法时, 如果发送缓冲没问题, 会返回正确写入(发送). 但发送的报文会导致对端发送RST报文, 因为对端的socket已经调用了close, 完全关闭, 既不发送, 也不接收数据. 所以, 第二次调用write方法(假设在收到RST之后), 会生成SIGPIPE信号, 导致进程退出.
https://blog.csdn.net/lmh12506/article/details/8457772













