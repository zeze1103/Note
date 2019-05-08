 Linux C语言



C特点： 操作系统/嵌入式硬件/高性能要求

# 一. 环境：

​	cc/gcc

# 二.gcc指令

​	gcc (-c) main.c -o main.out	编译main生成可执行的main.out

​	gcc -c a.c -o a.o	编译a.c生成a.o二进制文件	

​	gcc a.o b.o main.c -o main.out 	编译main.c依赖于a.o和b.o，生成main.out可执行文件，真样就可以先编译一些函数的二进制文件，再编译main.c

​	gcc main.c -o main.out && ./main.out	&& 用于连接两个指令，但是要求前一个文件的返回值必须是0

# 三.include:

​	#include <stdio.h>	引用系统自带的声明文件

​	#include "a.c"	相当于在当前函数中复制了一次a.c的所有代码

​	#include "a.h"	只引用对应的声明文件/头文件，这种方式在编译的时候必须指明所有以来的.o或.c文件

# 四.Makefile

​	hello.out:max.o min.o hello.c
​        	gcc max.o min.o hello.c -o hello.out
​	max.o:max.c
​        	gcc -c max.c
​	min.o:min.c
​      	  gcc -c min.c             	

​	递归的把所有相互依赖的文件都编译了

