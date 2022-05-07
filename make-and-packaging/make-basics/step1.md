在上一章中我们学习到了如何在linux环境下进行软件开发工作，以及如何将一个简单的程序编译成可执行文件，接下来我们将学习如何编译更复杂的程序。


## 任务

1. 执行 `[[cd chapter2]]{{RUN}}` 进入章节目录

2. 执行 `[[ls -l]]{{RUN}}` 查看当前目录中的文件情况:

    可以看到执行文档里面包含了 4 个源码文件，分别是 `main.c`、 `hello.c`、 `sin_value.c` 和 `cos_value.c` :

    `main.c`：主要目的是让用户输入角度数据与调用其他三个子程序

    `hello.c`：输出欢迎信息

    `sin_value.c`：计算使用者输入的角度（360）sin 数值

    `cos_value.c`：计算使用者输入的角度（360）cos 数值

3. 编译项目：
    
    执行 `[[gcc -c main.c hello.c sin_value.c cos_value.c]]{{RUN}}` 进行目标文件的编译，最终会有 4 个 *.o 的文件出现.

    执行 `[[gcc -o angle_cal main.o hello.o sin_value.o cos_value.o -lm]]{{RUN}}` 连结所有目标文件为执行文件，并加入 libm 的函数，产生名为 `angle_cal` 的执行文件

4. 执行程序并与程序进行交互，查看程序执行结果：

    执行 `[[./angle_cal]]{{RUN}}`

