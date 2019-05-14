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

# 五.C 语言与系统交互

C语言main的完整形式

```
int main(int argv, char* argc[])
{
	...
	return 0;
}
int argv 代表所有参数的个数，第一个为程序名
char* argc[] 代表所有传入的参数
```

如果这里return 的是1, 那么echo $? 就会显示1

```
echo $? 显示错误码
```

# 六.标准输入、输出流、错误流

stdio.h

```
#include <stdio.h>
/*
stdin
stdout
stderr
*/
int main()
{
        // printf();
        fprintf(stdout,"pease input the value a:\n");
        int a;
        // scanf("%d",&a);
        fscanf(stdin,"%d",&a);
        if(a<0){
                fprintf(stderr,"the value must > 0\n");
                return 1;
        }
        return 0;
}
```

linux 通道/管道

输入、输出、错误流的重定向机制

输出流重定向

```
./a.out 1>>a.txt 将输出流重定向到a.txt文件，这种方式不会覆盖原来的文件，会追加到文件末尾
这种方式在任何指令之后都可以使用
./a.out 1>>a.txt 一个单箭头的话就会覆盖源文件
```

输入流重定向

```
./a.out < input.txt
```

错误流重定向

```
./a.out 1>a.txt 2>f.txt 将正确的标准输入流重定向至a.txt,将错误流重定向至f.txt
```

# 七.Linux管道原理及应用

```
ls /etc/ | grep abc   | 代表管道，把前一个命令结果的输出流作为下一个命令的输入流
```

