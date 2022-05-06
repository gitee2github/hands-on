在学习几乎任何一款编程语言时，第一个示例通常是编写一个在屏幕上打印`Hello World!`的示例程序，在本节中我们同样通过使用C语言编写这样一个示例程序来进行相应的学习。

## 任务 

进入工作目录进行下一步学习：
`[[cd chapter1]]{{RUN}}`

1. 执行 `[[vi hello.c]]{{RUN}}` 创建并打开一个新的名为`hello.c`的C语言程序代码文件。

2. 在键盘上点击 `a` 或 `i` 或 `s` 进入编辑模式。

3. 将下面的内容输入到终端中：
```
#include <stdio.h>

int main(void){
    printf("Hello, World!\n");
}
```

4. 在键盘上点击 `ESC` ，然后输入 `:wq` 保存并退出Vim编辑器

这样，我们就通过Vim编辑器完成了 `hello.c` 代码的开发。

## Tips

更多有关Vim编辑器使用的学习内容，请参考：
https://www.vim.org/docs.php