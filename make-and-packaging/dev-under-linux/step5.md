在编译多个子程序所组成的程序时，需要首先将它们编译成目标文件(object)，再以连接制作为最终的可执行文件。

## 任务

将源文件编译为目标文件：

`[[gcc -c hello.c thanks.c]]{{RUN}}`

通过 `[[ls -l]]{{RUN}}` 观察目录变化， `*.o` 是上一条命令编译产生的新文件。

将 `hello.o` 与 `thanks.o` 共同编译成可执行文件 `thanks` :
`[[gcc -o thanks hello.o thanks.o]]{{RUN}}`

执行 `[[./thanks]]{{RUN}}` 并观察运行结果

执行 `[[cd ..]]{{RUN}}`返回到课程主目录

## Tips

更复杂的程序间调用通常需要制作 `.h` 头文件并在程序源代码最顶端以 `#include <xxx.h>` 进行引用。