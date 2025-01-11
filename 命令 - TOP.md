## 1. 作用

查看CPU、内存使用情况，类似于Windows的任务管理器。默认5秒钟刷新一次

交互式软件，启用后，可以通过快捷键控制

## 2. 语法

```shell
top [options]
```

`[options]`：

+ `[-p]`：只显示某个进程的信息
+ `[-d]`：显示刷新时间，默认是5s
+ `[-c]`：显示产生进程的完整命令，默认是程进程名
+ `[-n]`：显示刷新次数，需要参数为刷新次数
+ `[-b]`：以非交互非全屏式运行
+ `[-i]`：不显示任何闲置(idle)或无用进程
+ `[-u]`：查看特定用户启动的进程，需要参数为用户名

## 3. 界面信息

```shell
# 第一行
top - num1 up num2, num3 users, load average: num4, num5, num6
```

+ `num1`：系统时间
+ `num2`：系统启动时间
+ `num3`：用户数
+ `load average`：负载均衡
	+ 负载的数值为CPU使用率
+ `num4`, `num5`, `num6`：1分钟平均负载, 5分钟平均负载, 15分钟平均负载

第二行：进程信息

```shell
# 第二行
Tasks: num1 total, num2 runing, num3 sleeping, num4 stopped, num5 zombie
```

+ `Task`：进程

第三行：CPU信息

```shell
# 第三行
%Cpu(3): num1 us, num2 sy, num3 ni, num4 id, num5 wa, num6 hi, num7 si, num8 st
```

+ `us`：用户CPU使用率--important
+ `sy`：系统CPU使用率--important
+ `ni`：高优先级进程占用CPU时间百分比
+ `id`：空闲CPU率
+ `wa`：IO等待CPU占用率
+ `hi`：CPU硬件中断率
+ `si`：CPU软件中断率
+ `st`：强制等待占用CPU率

第四行：物理内存

```shell
# 第四行
KiB Men: num1 total, num2 free, num3 used, num4 buff/cache
```

+ `Kib Men`：物理内存

第五行：虚拟内存信息

```shell
# 第五行
KiB Swap: num1 total, num2 free, num3 used, num4 avail Men
```

+ `KiB Swap`：虚拟内存(交换空间)

第六行及以后行：进程详细信息

```shell
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
```

+ `PID`：进程ID
+ `USER`：进程所属用户
+ `PR`：进程优先级，越小越高
+ `NI`：负值是高优先级，正值表示低优先级
+ `VIRT`：虚拟内存
+ `RES`：物理内存
+ `SHR`：共享内存
+ `S`：状态
	+ `S`：sleep
	+ `R`：running
	+ `Z`：zombie
	+ `N`：负数优先级
	+ `I `：空闲状态
+ `%CPU`：进程占用CPU率
+ `%MEM`：进程占用内存率
+ `TIME+`：进程使用CPU时间总计，单位10毫秒

## 4. 快捷键

```shell
# 快捷键很多，只需要记住help快捷键
h
```
