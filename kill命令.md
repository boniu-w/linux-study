相信很多程序员对于Linux系统都不陌生，即使自己的日常开发机器不是Linux，那么线上服务器也大部分都是的，所以，掌握常用的Linux命令也是程序员必备的技能。

但是，怕就怕很多人对于部分命令只是一知半解，使用不当就能导致线上故障。

前段时间，我们的线上应用报警，频繁FGC，需要紧急处理问题，于是有同事去线上重启机器（正常程序应该是先采集堆dump，然后再重启，方便排查是否存在内存泄露等问题）。

但是在重启过程中，同事发现正常的重启命令应用无反应，然后尝试使用kill命令"杀"掉Java进程，但是仍然无效。于是他私自决定使用 "kill -9"结束了进程的生命。

虽然应用进程被干掉了，但是随之而来带来了很多问题，首先是上游系统突然发生大量报警，对应开发找过来说调用我们的RPC服务无响应，频繁超时。

后来，我们又发现系统中存在部分脏数据，有些在同一个事务中需要完整更新的数据，只更新了一半…

为什么正常的kill无法"杀掉"进程，而`kill -9`就可以？为什么`kill -9`会引发这一连串连锁反应？正常的kill执行时，JVM会如何处理的呢？

要搞清楚这些问题，我们要先从kill命令说起。

## **kill 命令**

我们都知道，想要**在Linux中终止一个进程有两种方式，如果是前台进程可以使用Ctrl+C键进行终止；如果是后台进程，那么需要使用kill命令来终止。**（其实Ctrl+C也是kill命令）

kill命令的格式是：

```text
kill[参数][进程号]

如：

kill 21121

kill -9 21121
```

其中[参数]是可选的，进程号可以通过jps/ps/pidof/pstree/top等工具获取。

kill的命令参数有以下几种：

> -l 信号，若果不加信号的编号参数，则使用“-l”参数会列出全部的信号名称
> -a 当处理当前进程时，不限制命令名和进程号的对应关系
> -p 指定kill 命令只打印相关进程的进程号，而不发送任何信号
> -s 指定发送信号
> -u 指定用户

通常情况下，我们使用的`-l`(信号)的时候比较多，如我们前文提到的`kill -9`中的`9`就是信号。

信号如果没有指定的话，默认会发出终止信号(15)。常用的信号如下：

> HUP 1 终端断线
> INT 2 中断（同 Ctrl + C）
> QUIT 3 退出（同 Ctrl + \）
> TERM 15 终止
> KILL 9 强制终止
> CONT 18 继续（与STOP相反， fg/bg命令）
> STOP 19 暂停（同 Ctrl + Z）

比较常用的就是`强制终止信号：9`和`终止信号：15`，另外，`中断信号：2`其实就是我们前文提到的Ctrl + C结束前台进程。

那么，`kill -9` 和 `kill -15`到底有什么区别呢？该如何选择呢？

## **kill -9 和 kill -15的区别**

kill命令默认的信号就是15，首先来说一下这个默认的`kill -15`信号。

当使用`kill -15`时，系统会发送一个SIGTERM的信号给对应的程序。当程序接收到该信号后，具体要如何处理是自己可以决定的。

这时候，应用程序可以选择：

- 1、立即停止程序
- 2、释放响应资源后停止程序
- 3、忽略该信号，继续执行程序

因为`kill -15`信号只是通知对应的进程要进行"安全、干净的退出"，程序接到信号之后，退出前一般会进行一些"准备工作"，如资源释放、临时文件清理等等，如果准备工作做完了，再进行程序的终止。

但是，如果在"准备工作"进行过程中，遇到阻塞或者其他问题导致无法成功，那么应用程序可以选择忽略该终止信号。

这也就是为什么我们有的时候使用kill命令是没办法"杀死"应用的原因，因为**默认的kill信号是SIGTERM（15），而SIGTERM（15）的信号是可以被阻塞和忽略的。**

和`kill -15`相比，`kill -9`就相对强硬一点，系统会发出SIGKILL信号，他要求接收到该信号的程序应该立即结束运行，不能被阻塞或者忽略。

所以，**相比于kill -15命令，kill -9在执行时，应用程序是没有时间进行"准备工作"的，所以这通常会带来一些副作用，数据丢失或者终端无法恢复到正常状态等。**

**Java是如何处理SIGTERM（15）的**我们都知道，在Linux中，Java应用是作为一个独立进程运行的，Java程序的终止运行是基于JVM的关闭实现的，JVM关闭方式分为3种：

> 正常关闭：当最后一个非守护线程结束或者调用了System.exit或者通过其他特定平台的方法关闭（接收到SIGINT（2）、SIGTERM（15）信号等）强制关闭：通过调用Runtime.halt方法或者是在操作系统中强制kill（接收到SIGKILL（9）信号)异常关闭：运行中遇到RuntimeException异常等。

JVM进程在接收到`kill -15`信号通知的时候，是可以做一些清理动作的，比如删除临时文件等。

当然，开发者也是可以自定义做一些额外的事情的，比如让tomcat容器停止，让dubbo服务下线等。

而这种**自定义JVM清理动作的方式，是通过JDK中提供的shutdown hook实现的。JDK提供了Java.Runtime.addShutdownHook(Thread hook)方法，可以注册一个JVM关闭的钩子。**例子如下：

```text
package com.hollis;


public class ShutdownHookTest {


    public static void main(String[] args) {

        boolean flag = true;

        Runtime.getRuntime().addShutdownHook(new Thread(() -> {

            System.out.println("hook execute...");

        }));


        while (flag) {

            // app is runing

        }


        System.out.println("main thread execute end...");

    }

}
```

执行命令：

```text
➜ jps

6520 ShutdownHookTest

6521 Jps

➜ kill 6520
```

控制台输出内容：

```text
hook execute...

Process finished with exit code 143 (interrupted by signal 15: SIGTERM)
```

可以看到，当我们使用kill（默认kill -15）关闭进程的时候，程序会先执行我注册的shutdownHook，然后再退出，并且会给出一个提示：`interrupted by signal 15: SIGTERM`

如果我们执行命令`kill -9`：

```text
➜ kill -9 6520
```

控制台输出内容：

```text
Process finished with exit code 137 (interrupted by signal 9: SIGKILL)
```

可以看到，当我们使用kill -9 强制关闭进程的时候，程序并没有执行shutdownHook，而是直接退出了，并且会给出一个提示：`interrupted by signal 9: SIGKILL`

## **总结**

kill命令用于终止Linux进程，默认情况下，如果不指定信号，kill 等价于`kill -15`。

`kill -15`执行时，系统向对应的程序发送SIGTERM（15）信号，该信号是可以被执行、阻塞和忽略的，所以应用程序接收到信号后，可以做一些准备工作，再进行程序终止。

有的时候，`kill -15`无法终止程序，因为他可能被忽略，这时候可以使用`kill -9`，系统会发出SIGKILL（9）信号，该信号不允许忽略和阻塞，所以应用程序会立即终止。

这也会带来很多副作用，如数据丢失等，所以，在非必要时，不要使用`kill -9`命令，尤其是那些web应用、提供RPC服务、执行定时任务、包含长事务等应用中，因为`kill -9`没给spring容器、tomcat服务器、dubbo服务、流程引擎、状态机等足够的时间进行收尾。