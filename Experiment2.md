# 实验二 栈和队列的应用

1.算术表达式求值：利用栈实现一个中缀表达式的求值

代码如下：
```c

```

2.停车场模拟：利用栈实现单道停车场，也就是该停车场先进来的车只能最后出，如果某辆车想出车道，必须先把其前面的车先退出栈，等该车开走，再将之前的车压入栈。输入文件如附件文件中data.txt所示，其中格式如：“COOLONE arrives”，表示COOLONE的车到达；输出如文件outpu.txt所示，其中格式为：“COOLONE was moved 0 times while it was here”，表示该车在离开之前没有移动过。

代码如下：
```c

```

3.打印机模拟：利用队列模拟打印机的打印功能。打印机要处理一系列打印任务，其中打印任务列表在附件文件bigfirst.run中，其中格式如：“1 100 giraffe”，表示第一个任务的发起人是giraffe，共有100页。输出文件如bigfirst.out中，其中格式为“Arriving: 100 pages from giraffe at 1 seconds”表示giraffe的作业任务在1秒的时候到达。“Servicing: 100 pages from giraffe at 1 seconds”表示giraffe的作业在1秒的时候被打印了。可能会出现某个作业到达时，打印机并不空闲，那么该作业需要等待，并统计总的等待时间和平均延迟。

代码如下：
```c

```

[下一个实验](/Experiment3.md)

[返回首页](/README.md)
