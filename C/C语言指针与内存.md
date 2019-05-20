# C语言指针与内存

## 初始指针

```
*a	指针		去a的内存地址中的值
&a	取地址
void change(int a, int b){}		只将变量的值传递进函数

void change(int *a, int *b){}		传递变量的地址
```

## GDB

```
gcc -g main.c -o main.out 	这样生成的main.out可以调试
```

gdb 指令

```
list/l 显示代码
start 开始执行
print/p a 打印变量a
next/n	执行下一行
s	进入当前函数
bt 查看函数堆栈
f 1	切换函数堆栈到1
```

