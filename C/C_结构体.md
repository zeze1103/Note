# C_结构体

## 预处理

1. 编译过程：
   1. .c文件-.i文件（预处理）
   2. -.s文件（编译）
   3. -.o文件（汇编）
   4. -可执行文件（链接）
   
2. 预处理：

   1. 展开头文件
   2. 宏替换: 预处理阶段单纯的字符串替换 ，他把红定义里的变量作为字符串替换到程序中位置
   3. 条件编译
   4. 预处理阶段宏不考虑编译器语法，就是字符串替换

3. 宏定义：

   ```
   #define R 10
   ```

4. 宏函数

   ```
   #define N(n) n*10
   ```

   宏函数不会对变量类型做限制

5. typedef

   1. 给变量类型起别名

      ```
      typedef int tni;
      ```

   2. typedef在预处理过程中不会被替换

   3. size_t是typedef unsigned long size_t

   4. 他经常用于给结构体起别名

   5. typedef有作用域，只能作用于自己定义的函数中

## 结构体

​	结构体对象内存大小：

1. 结构提声明和定义

   1. 结构体是不同类型变量的集合

   2. ```
      1.
      struct weapon{
              char name[20];
              int atk;
              int price;
      };
      struct weapon weapon_1;
      2.struct weapon{
              char name[20];
              int atk;
              int price;
      }weapon_1;
      
      3. struct{
              char name[20];
              int atk;
              int price;
      }weapon_1;
      ```

2. 初始化和引用

   ```
   struct weapon weapon_1 ={"weapon_name",100,200} ;
   ```

   结构体数组

   ```
   struct weapon weapon_2[2]={{"weapon_name1",50,100},{"weapon_name2",100,200}};
   ```

3. 结构体指针

   ```
           struct weapon *w;
           w=&weapon_1;
           (*w).name,w->name均可访问name
   ```

4. 共用体

   关键字：union

   作用：使几个不同类型变量共享同一个内存地址

   优点：节省开销

   缺点：同一时刻只能存储一个成员

   内存：共用体内存长度是所有成员中最长的成员的内存长度，共用体变量的地址和其中所有成员的地址都是同一个地址

## 动态数据结构

### 静态链表

```
#include <stdio.h>
struct weapon {
        int price;
        int atk;
        struct weapon *next;
};


int main(){
        struct weapon a,b,c,*head;
        a.price =100;
        a.atk =100;
        b.price = 200;
        b.atk =200;
        c.price =300;
        c.atk = 300;
        head = &a;
        a.next = &b;
        b.next = &c;
        c.next = NULL;


        struct weapon *p;
        p = head;
        while(p!=NULL){
                printf("%d,%d\n",p->atk,p->price);
                p=p->next;
        }
        return 0;
}
```

malloc 分配内存块的函数

sizeof判断数据了行长度符

### 动态链表

```
#include <stdio.h>
#include <malloc.h>
struct weapon {
        int price;
        int atk;
        struct weapon * next;
};

struct weapon * create(){
        struct weapon *head;
        struct weapon *p1,*p2;
        int n =0;
        p1 = p2=(struct weapon*)malloc(sizeof(struct weapon));
        scanf ("%d,%d",&p1->price,&p1->atk);
        head = NULL;
        while (p1->price!=0){
                n++;
                if (n==1) head=p1;
                else p2->next=p1;
                p2=p1;
                p1 = (struct weapon*)malloc(sizeof(struct weapon));
                scanf("%d,%d",&p1->price,&p1->atk);
        }
        p2->next = NULL;
        return (head);
}


int main(){
        struct weapon *p;
        p=create();
        printf("%d,%d",p->price,p->atk);
        return 0;
}
```

## 位运算 & | ^ ~ << >>

### 按位与 &

将参与运算的两个数据按照对应的二进制数逐位进行逻辑与运算，参与运算的数必须是整形或字符型，而且必须要以补码的方式进行出现

应用：

1. 迅速清零

2. 保留数据的指定位

   ```
   int c = a&0xFF;
   ```

### 按位或 |

设定数据的指定位置

```
int c = a|0xFF;
```

### 按位异或 ^

数值交换

```
a = a^b;
b=b^a;
a=a^b;
```

定位翻转



### 按位取反 ~

唯一的单目运算符，具有右结合性

### 左移、右移 << >>

高位丢弃、低位补零

作用：×或/2的n次方

注意：int 是有符号的类型，左移过程会导致最左端符号位被丢弃

​			若当前数据是有符号数，右移过程中会根据符号位进行判断决定补0或1



## 递归调用

原理：

1. 函数调用：
   1. 为形参分配临时内存单元，将实参的值传递进去，同时将主函数返回地址/当前地址传递进去（保护现场）
   2. 回到主调函数的过程中，将返回值返回到之前储存的返回地址，释放形参存储单元
   3. 这些东西都是保存在栈里面   
2. 递归调用：
   1. 所有被调用函数都会创建一个副本，为各自的调用者服务，而不受其他函数的影响。被调用了多少次就会创建多少个副本。
   2. 一般都会有边界条件

