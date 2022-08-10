---
title: C  编译过程
date: 2022-03-01
tags:

---

我是短小精悍的文章摘要(๑•̀ㅂ•́) ✧

<!-- more -->

下面将通过一个简单的 “Hello World” C 代码演示C编译的过程

```c
#include<stdio.h>

int main(int argc, char const *argv[]){
    printf("Hello World!");
    return 0;
}
```

C

C 代码的编程分为四步：

- 预处理
- 编译
- 汇编
- 链接

## 预处理（Preprocessing）

通过 Gcc 指令添加 -E 选项，即可控制GCC 编译器仅对源代码做预处理操作。

值得注意的是，默认情况下 gcc -E 指令只会将预处理操作的结果输出到屏幕上，并不会自动保存到某个文件。因此该指令往往会和 -o 选项连用，将结果导入到指令的文件中。比如

```bash
➜  C_module1 ls
main.c
➜  C_module1 cat main.c             
#include<stdio.h>

int main(int argc, char const *argv[]){
    printf("Hello World!");
    return 0;
}
➜  C_module gcc -E main.c -o main.i
➜  C_module ls         
main.c  main.i
```

Bash

Linux 系统中通常用 “.i” 作为 C 语言程序预处理后所得文件的后缀名。由此，就完成了 demo.c 文件的预处理操作，并将其结果导入到了 demo.i 文件中。

## 编译（Compilation）

通过给 gcc 指令添加 -S（注意是大写）选项，即可令 GCC 编译器仅将指定文件加工至编译阶段，并生成对应的汇编代码文件。

```bash
➜  C_module1 gcc -S main.i          
➜  C_module1 ls
main.c  main.i  main.s
➜  C_module1 vim main.s 
➜  C_module1 
```

Bash

## 汇编

汇编阶段就是将之前生成的汇编代码文件（main.s）做进一步转换，生成对应的机器指令。通过给 gcc 指令添加 -c 选项，即可令 GCC 编译器仅对指定的汇编代码文件做汇编操作。

```bash
➜  C_module1 gcc -c main.s 
➜  C_module1 ls
main.c  main.i  main.o  main.s
```

Bash

## 链接

目标文件已经是二进制文件，与可执行文件的组织形式类似，只是有些函数和全局变量的地址还未找到，因此还无法执行。链接的作用就是找到这些目标地址，将所有的目标文件组织成一个可以执行的二进制文件。

完成链接操作，并不需要给 gcc 添加任何选项，只要将汇编阶段得到的 main.o 作为参数传递给它，gcc就会在其基础上完成链接操作。例如：

```bash
➜  C_module1 gcc main.o        
➜  C_module1 gcc main.o -o main
➜  C_module1 rm a.out 
➜  C_module1 ls
main  main.c  main.i  main.o  main.s
```

Bash

## 总结

| **操作** | **源文件** | **目标文件**            | **Gcc 命令**            |
| -------- | ---------- | ----------------------- | ----------------------- |
| 预处理   | main.c     | main.i                  | gcc -E main.c -o main.i |
| 编译     | main.i     | main.s （汇编代码文件） | gcc -S main.i           |
| 汇编     | main.s     | main.o                  | gcc -c main.s           |
| 链接     | main.o     | main                    | gcc main.o -o main      |