可以看到，相对与第一章中程序的编译，刚才的编译指令就变得复杂起来了，如果要重新编译，上述流程还需要重新来一次。对于更为复杂的项目来说，这样操作不仅麻烦，还容易出错。

可以使用 `make` 工具简化我们的工作，`make` 工具执行时，需要一个 `Makefile` 文件，以告诉 `make` 工具需要怎么样的去编译和链接程序。

## 任务 

1. 执行 `[[vi Makefile]]{{RUN}}` 为项目创建 `Makefile`。

2. 在键盘上点击 `a` 或 `i` 或 `s` 进入编辑模式。

3. 将下面的内容输入到终端中：
    ```
    main: main.o hello.o sin_value.o cos_value.o
        gcc -o main main.o hello.o sin_value.o cos_value.o -lm
    ```
    注意第 2 行数据，是按 `TAB` 键产生的空格

4. 在键盘上点击 `ESC` ，然后输入 `:wq` 保存并退出Vim编辑器

这样，我们就通过Vim编辑器完成了 `Makefile` 的编写。

## Tips

`Makefile` 的语法多而复杂，可以参考 GUN 官网文档，这里仅做一些基本的介绍：

在 makefile 中的规则基本上是：

`\#` 代表批注

`<tab>` 需要在命令行的第一个字符

目标 target 与相依文件（目标文件）之间以 `:` 分割

例如：

```
目标（target）：目标文件1 目标文件2
<tab>	 gcc -o 欲建立的执行文件 目标文件1 目标文件2
```