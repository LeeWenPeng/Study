## 1. ss 介绍

`ss` （socket statistics）是一个强大的网络工具，用于显示和分析 Linux 系统的套接字信息。相比 netstat，ss 更加高效、功能强大，并且是现代 Linux 系统的默认选择。

`ss` 的优势：

+ 与`netstat` 相比，`ss` 的优势在于它能够显示更多更详细的有关 `TCP` 和连接状态的信息，而且比 `netstat` 更快速更高效。
+ 当服务器的 `socket` 连接数量变得非常大时，使用 `netstat` 命令和 `cat /proc/net/tcp`执行速度很慢，而 `ss` 才是推荐的。

>[!tip] `ss` 快的秘诀，在于用到了`TCP`协议栈中的`tcp_diag`
>`tcp_diag` 是一个用于分析统计的模块，可以获得 `Linux` 内核中第一手的信息，这就确保了 `ss` 的快捷高效。当然，如果你的系统中没有 `tcp_diag`，ss也可以正常运行，只是效率会变得稍慢。

## 2. ss 语法

```shell
ss [options] [FILTER]
```

+ options：控制显示内容
+ FILTER：也能够与筛选套接字信息

## 3. options

| 选项                                  | 描述                        | 补充  |
| ----------------------------------- | ------------------------- | --- |
| `-h, --help`                        | 帮助信息                      |     |
| `-V, --version`                     | 程序版本信息                    |     |
| `-n, --numeric`                     | 不解析服务名称，显示数字格式的端口和地址      |     |
| `-r, --resolve`                     | 解析 ip 地址为主机名              |     |
| `-a, --all`                         | 显示所有套接字，包括监听和非监听状态        |     |
| `-l, --listening`                   | 显示监听状态的套接字                |     |
| `-o, --options`                     | 显示计时器信息                   |     |
| `-e, --extended`                    | 显示详细的套接字信息                |     |
| `-m, --memory`                      | 显示套接字的内存使用情况              |     |
| `-p, --processes`                   | 显示使用套接字的进程信息              |     |
| `-i, --info`                        | 显示 TCP 内部信息和更多详细信息        |     |
| `-s, --summary`                     | 显示套接字使用概况                 |     |
| `-4, --ipv4`                        | 仅显示IPv4的套接字               |     |
| `-6, --ipv6`                        | 仅显示IPv6的套接字               |     |
| `-0, --packet`                      | 显示 PACKET 套接字             |     |
| `-t, --tcp`                         | 仅显示 TCP 套接字               |     |
| `-u, --udp`                         | 仅显示 UCP 套接字               |     |
| `-d, --dccp`                        | 仅显示 DCCP套接字               |     |
| `-w, --raw`                         | 仅显示 RAW 套接字               |     |
| `-x, --unix`                        | 仅显示 Unix 套接字              |     |
| `-f, --family=FAMILY`               | 显示 FAMILY类型的套接字           | 补充1 |
| `-A, --query=QUERY, --socket=QUERY` |                           | 补充2 |
| `-D, --diag=FILE`                   | 将原始TCP套接字（sockets）信息转储到文件 |     |
| `-F, --filter=FILE`                 | 从文件中都去过滤器信息               | 补充3 |

> [!note] 补充1
> FMAILY 可选，支持 unix, inet, inet6, link, netlink

>[!note] 补充2
`QUERY := {all|inet|tcp|udp|raw|unix|packet|netlink}[,QUERY]`

>[!note] 补充3
>`FILTER := [ state TCP-STATE ] [ EXPRESSION ]`

## 4. FILTER

TCP 状态

+ `established`
+ `syn-sent`
+ `syn-recv`
+ `fin-wait-1`
+ `fin-wait-2`
+ `time-wait`
+ `closed`
+ `close-wait`
+ `last-ack`
+ `listening`
+ `closing`

其他状态：

+ `all`：列出所有的 TCP 状态。
+ `connected`：列出除了 listening 和 closing 之外的所有 TCP 状态。
+ `synchronized`：列出除了 syn-sent 之外的所有 TCP 状态。
+ `bucket`：列出 maintained 的状态，如：time-wait 和 syn-recv。
+ `big`：列出和 bucket 相反的状态。

## 5. 过滤器

按源ip地址过滤

```shell
# 匹配本地 ip 和端口号
ss dst ip:port
```

按目的 ip 地址过滤

```shell
# 匹配远程 ip 和端口号
ss dst ip:port
```

按端口号过滤

```shell
ss dport options PORT
ss sport options PORT
```

options：

+ `<` / `lt`
+ `>` / `gt`
+ `<=` / `le`
+ `>=` / `ge`
+ `==` / `eq`
+ `!=` / `ne`

## 6. 同时过滤TCP状态和端口号

单条件过滤

```shell
ss state FILTER_NAME dport options PORT
```

多条件过滤（带括号）

```shell
ss state FILTER_NAME \( dport options PORT  or dport options PORT2 \)

ss state FILTER_NAME '( dport options PORT  and dport options PORT2 )'
```

+ 括号用于分组条件
+ 可以使用转义字符`\(`和`\)`
+ 推荐使用单引号，以避免使用转义字符

## 7. 学习网址

[ss 学习网址](https://kklinux.github.io/linux-command/c/ss.html)
