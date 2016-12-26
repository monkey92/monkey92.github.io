
gcc 命令

-o 输出文件名

-O -o0 -o1 -o2 -o3 编译优化

-g -g0 -g1 -g2 -g3 产生调试信息

-Wall 显示所有警告
-Werror 把警告当错误显示
-w 关闭所有警告

-c 只编译不连接
-S 编译成汇编文件
-E 预编译
-D 编译时候定义宏  gcc main.c -DNUM=1024
--------------------------
# 编译静态库
 gcc -c -static foo.c
 gcc -c -static bar.c

ar  -r 指定静态库文件 目标文件
	-t 

ar -r tool.a foo.o bar.o //生成 too.a

nm  静态库 | 动态库 | 目标文件 | 执行文件 (查看函数符号表)

# 使用静态库编译
gcc main.c tool.a -o main 

# 动态库(共享库)
动态库可以执行，静态库不可以执行
动态库没有main 不能独立执行
动态库不会连接成程序的一部分
程序执行的时候，必须需要动态库文件

命令 ldd 查看程序调用的动态库，只可以查看可执行文件


readelf -h <可执行文件> 查看可执行文件的ELF格式 的头信息


# 动态库的编译
gcc -c
	-fpic (可选)
	--shared  （连接） 
//得到目标文件
gcc -c -fpic too1.c
gcc -c -fpic too2.c
//得到动态库文件
gcc -shared -olibtool.so too1.o too2.o


# 使用动态库

gcc foo.c -ltool -L . -omain

-l 库名 不用加前缀lib 也不用 加后缀 .so
-L 库路径
-----------------------------

库名的命名约定
lib库名.a
lib库名.so

-----------------------------

约定文件后缀
.c c源代码文件
.cpp .cc .hpp  c++源代码文件
.h 头文件
.o 目标文件
.a 静态库文件
.so 动态库文件
.i 预编译文件
.s 汇编文件

----------
dlopen  打开一个动态库
dlsym 在打开动态库找一个函数
dlclose 关闭动态库
dlerror 返回错误信息
