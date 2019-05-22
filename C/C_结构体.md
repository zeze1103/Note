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
struct weapon {
        int price;
        int atk;
        struct weapon *next;
};
```

malloc 分配内存块的函数

sizeof判断数据了行长度符