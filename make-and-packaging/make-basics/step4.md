对上这个示例，如果有两个以上的执行动作时，如何做？比如增加一个指令，直接清除所有的目标文件与执行文件。

## 任务

1. 执行 `[[vi Makefile]]{{RUN}}` 再次打开`Makefile`文件。

2. 使用键盘上的方向键将光标移动到文件的结尾。

3. 在键盘上点击 `a` 或 `i` 进入编辑模式。

4. 修改文件内容为：
    ```
    main: main.o hello.o sin_value.o cos_value.o
        gcc -o main main.o hello.o sin_value.o cos_value.o -lm

    clean:
        rm -rf main.o hello.o sin_value.o cos_value.o
    ```

5. 在键盘上点击 `ESC` ，然后输入 `:wq` 保存并退出Vim编辑器


6. 执行：

    `[[make clean]]{{RUN}}` 清除所有 `*.o` 文件

    `[[ls -l]]{{RUN}}` 观察目录结果

7. 返回课程目录：
    执行 `[[cd ..]]{{RUN}}`
