# GDB介绍
<pre>
 GDB是GNU开源组织发布的一个强大的UNIX下的程序调试工具。或许，各位比较喜欢那种图形界面方式的，像VC、BCB等IDE的调试，但如果你是在UNIX平台下做软件，你会发现GDB这个调试工具有比VC、BCB的图形化调试器更强大的功能。所谓“寸有所长，尺有所短”就是这个道理。
    一般来说，GDB主要帮忙你完成下面四个方面的功能：

（1）启动你的程序，可以按照你的自定义的要求随心所欲的运行程序。
（2）可让被调试的程序在你所指定的调置的断点处停住。（断点可以是条件表达式）
（3）当程序被停住时，可以检查此时你的程序中所发生的事。
（4）动态的改变你程序的执行环境。
</pre>


# debug和release的区别
> Debug 通常称为调试版本，它包含调试信息，并且不作任何优化，便于程序员调试程序。Release 称为发布版本，它往往是进行了各种优化，使得程序在代码大小和运行速度上都是最优的，以便用户很好地使用。

> debug跟release在初始化变量时所做的操作是不同的，debug是将每个字节位都赋成0xcc， 而release的赋值近 似于随机(我想是直接从内存中分配的，没有初始化过)。这样就明确了，如果你的程序中的某个变量没被初始化就被引用，就很有可能出现异常：用作控制变量将 导致流程导向不一致；用作数组下标将会使程序崩溃；更加可能是造成其他变量的不准确而引起其他的错误。所以在声明变量后马上对其初始化一个默认的值是最简 单有效的办法，否则项目大了你找都没地方找。代码存在错误在debug方式下可能会忽略而不被察觉到，如debug方式下数组越界也大多不会出错，在 release中就暴露出来了，这个找起来就比较难了。

> Debug版本就是调试版本。在Debug版本中，可以使用单步执行、跟踪等功能，但其生成的可执行文件比较大，代码运行比较慢。Release版本就是发行版本，其运行速度较快，可执行文件较小，但在其编译条件下无法执行调试功能。还有一点，Release版本的exe文件链接的目标是标准的MFC DLL(Use MFC in a shared or static dll)。比如MFC42.DLL。这些DLL在安装windows的时候，就会装到系统中。因此，这样的exe在没有安装VS的机器上也能运行。而Debug版本的exe链接了调试版本的MFC DLL文件，比如MFC42.DLL。在没有安装VS的机器上不能运行，因为缺少MFC42D.DLL等，除非选择use static dll when link。  
 
>Debug版本中包含大量的调试信息，所以我们能够单步执行、Watch表达式等等，而release版本仅包含我们的代码。由于要利于程序的测 试，Debug版本的程序附带很多测试信息和测试程序时才需要的代码，所以Debug版本的程序需要VS的Debug（注意这里不是指程序的Debug， 而是指VS的调试器）才能运行。而Release版本就不具有这些特性，所以在Release版本的程序上不能做调试！打包就相当于将你制作的东西发布出 去，应该是优化过的代码，当然要用发布版本，即Release版本。 

>两者所用的动态连接库是不一样的,Release版本所需要的dll和lib已经包含在Windows的system(或者system32)下，所以只 需要拷贝就可以运行了，但是Debug版本需要的dll和lib是在安装VS时装上去的，如果你想直接将debug版本给用户，需要拷贝几个文件，但这样显得很臃肿，一般来说不可取。

# 基本使用hello world


```cpp
#include <iostream> 
using namespace std;
 
int func(int n){
	int sum=0;
	for(int i=0; i<n; i++){
		sum+=i;
	}
	return sum;
}
 
int main(){
	long result = 0;
	for(int i=1; i<=100; i++){
		result += i;
	}
	cout<<"result[1-100] = "<<result<<endl;
	cout<<"result[1-250] = "<<func(250)<<endl;
}
```


> 编译生成执行文件：<br>
g++ -g main.cpp -o main    # 编译时加上-g选项表示debug模式

> 使用GDB调试：<br>
gdb main

<br>
<br>

> GDB调试命令：<br>
<br>
> (gdb) l     <-------------------- l命令相当于list，从第一行开始例出原码。
```cpp
       #include <iostream>
       using namespace std;

       int func(int n){
               int sum=0;
               for(int i=0; i<n; i++){
                       sum+=i;
               }
               return sum;
      }
```
<br>
<br>

> (gdb)       <-------------------- 直接回车表示，重复上一次命令
```cpp

      int main(){
              long result = 0;
              for(int i=1; i<=100; i++){
                      result += i;
              }
              cout<<"result[1-100] = "<<result<<endl;
              cout<<"result[1-250] = "<<func(250)<<endl;
      }
```
<br>
<br>

> (gdb) break 16      <---------------------------- 在16行出设置断点<br>
Breakpoint 1 at 0x400941: file main.cpp, line 16.<br>
<br>
> (gdb) break func  <-------------------- 设置断点，在函数func()入口处。<br>
Breakpoint 2 at 0x4008ed: file main.cpp, line 5.\
<br>
> (gdb) info break  <-------------------- 查看断点信息。<br>
```
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x0000000000400941 in main() at main.cpp:16
2       breakpoint     keep y   0x00000000004008ed in func(int) at main.cpp:5
```
<br>

> (gdb) r           <--------------------- 运行程序，run命令简写<br>
Starting program: /home/xlmou/Codes/gdb/main <br>
Breakpoint 1, main () at main.cpp:17<br>
```cpp
17              cout<<"result[1-100] = "<<result<<endl;
```

> (gdb) n          <--------------------- 单条语句执行，next命令简写。<br>
> result[1-100] = 5050<br>
```cpp
18              cout<<"result[1-250] = "<<func(250)<<endl;
```

> (gdb) c          <--------------------- 继续运行程序，continue命令简写。<br>
Continuing.
```cpp
Breakpoint 2, func (n=250) at main.cpp:5
5               int sum=0;
```


> (gdb) n <--------------------- 单条语句执行，next命令简写。<br>
> (gdb) n<br>
```cpp
6               for(int i=0; i<n; i++){
```
> (gdb) <br>
```cpp
7                       sum+=i;
```
(gdb) n<br>
```cpp
6               for(int i=0; i<n; i++){
```
(gdb) n<br>
```cpp
7                       sum+=i;
```
(gdb) n<br>
```cpp
6               for(int i=0; i<n; i++){
```
(gdb) n<br>
```cpp
7                       sum+=i;
```
> (gdb) p i        <--------------------- 打印变量i的值，print命令简写。<br>
```cpp
$1 = 2
```
> (gdb) p sum        <--------------------- 打印变量i的值，print命令简写。<br>
```cpp
$2 = 1
```
> (gdb) bt        <--------------------- 查看函数堆栈。<br>
```cpp
#0  func (n=250) at main.cpp:6
#1  0x0000000000400979 in main () at main.cpp:18
```
> (gdb) finish    <--------------------- 退出函数。<br>
```cpp
Run till exit from #0  func (n=250) at main.cpp:6
0x0000000000400979 in main () at main.cpp:18
18              cout<<"result[1-250] = "<<func(250)<<endl;
Value returned is $6 = 31125
```
> (gdb) c     <--------------------- 继续运行。<br>
Continuing.
```cpp
result[1-250] = 31125
[Inferior 1 (process 2116) exited normally]
```

> (gdb) q     <--------------------- 退出gdb。


# GDB调试命令总结
### （1）启动GDB
一般来说GDB主要调试的是C/C++的程序。要调试C/C++的程序，首先在编译时，我们必须要把调试信息加到可执行文件中。使用编译器（cc/gcc/g++）的 -g 参数可以做到这一点。如：<br>
> cc -g hello.c -o hello<br>
> g++ -g hello.cpp -o hello<br>

果没有-g，你将看不见程序的函数名、变量名，所代替的全是运行时的内存地址。当你用-g把调试信息加入之后，并成功编译目标代码以后，让我们来看看如何用gdb来调试他。启动GDB的方法有以下几种：<br>
```
1）调试可执行文件:
$gdb <program>       # program也就是你的执行文件，一般在当前目录下。
2）调试core文件(core是程序非法执行后core dump后产生的文件):
$gdb <program> <core dump file>
$gdb program core.11127
3）调试服务程序:
$gdb <program> <PID>
$gdb hello 11127
```

如果你的程序是一个服务程序，那么你可以指定这个服务程序运行时的进程ID。gdb会自动attach上去，并调试他。program应该在PATH环境变量中搜索得到。

### （2）GDB交互命令
<pre>
 启动gdb后，进入到交互模式，通过以下命令完成对程序的调试；注意高频使用的命令一般都会有缩写，熟练使用这些缩写命令能提高调试的效率；

1）运行：
run：简记为 r ，其作用是运行程序，当遇到断点后，程序会在断点处停止运行，等待用户输入下一步的命令；
continue （简写c ）：继续执行，到下一个断点处（或运行结束）；
next：（简写 n），单步跟踪程序，当遇到函数调用时，也不进入此函数体；此命令同 step 的主要区别是，step 遇到用户自定义的函数，将步进到函数中去运行，而 next 则直接调用函数，不会进入到函数体内。
step （简写s）：单步调试如果有函数调用，则进入函数；与命令n不同，n是不进入调用的函数的
until：当你厌倦了在一个循环体内单步跟踪时，这个命令可以运行程序直到退出循环体。
until+行号： 运行至某行，不仅仅用来跳出循环
finish： 运行程序，直到当前函数完成返回，并打印函数返回时的堆栈地址和返回值及参数值等信息。
call 函数(参数)：调用程序中可见的函数，并传递“参数”，如：call gdb_test(55)
quit：简记为 q ，退出gdb

2）设置断点：
break n （简写b n）:在第n行处设置断点，（可以带上代码路径和代码名称： b OAGUPDATE.cpp:578）；
b line-or-function if a＞b：条件断点设置；
break func（break缩写为b）：在函数func()的入口处设置断点，如：break cb_button；
delete 断点号n：删除第n个断点；
disable 断点号n：暂停第n个断点；
enable 断点号n：开启第n个断点；
clear 行号n：清除第n行的断点；
info b （info breakpoints） ：显示当前程序的断点设置情况；
delete breakpoints：清除所有断点；

3）查看源代码：
list ：简记为 l ，其作用就是列出程序的源代码，默认每次显示10行；
list 行号：将显示当前文件以“行号”为中心的前后10行代码，如：list 12；
list 函数名：将显示“函数名”所在函数的源代码，如：list main；
list ：不带参数，将接着上一次 list 命令的，输出下边的内容。

4）打印表达式：
print 表达式：简记为 p ，其中“表达式”可以是任何当前正在被测试程序的有效表达式，比如当前正在调试C语言的程序，那么“表达式”可以是任何C语言的有效表达式，包括数字，变量甚至是函数调用；
print a：将显示整数 a 的值；
print ++a：将把 a 中的值加1,并显示出来；
print name：将显示字符串 name 的值；
print gdb_test(22)：将以整数22作为参数调用 gdb_test() 函数；
print gdb_test(a)：将以变量 a 作为参数调用 gdb_test() 函数；
display 表达式：在单步运行时将非常有用，使用display命令设置一个表达式后，它将在每次单步进行指令后，紧接着输出被设置的表达式及值。如： display a；
watch 表达式：设置一个监视点，一旦被监视的“表达式”的值改变，gdb将强行终止正在被调试的程序。如： watch a；
whatis ：查询变量或函数；
info function： 查询函数；
扩展info locals： 显示当前堆栈页的所有变量；

5）查询运行信息：
where/bt ：当前运行的堆栈列表；
bt backtrace 显示当前调用堆栈；
up/down 改变堆栈显示的深度；
set args 参数:  指定运行时的参数；
show args： 查看设置好的参数；
info program： 来查看程序的是否在运行，进程号，被暂停的原因。

6）分割窗口：
layout： 用于分割窗口，可以一边查看代码，一边测试：
layout src：显示源代码窗口；
layout asm：显示反汇编窗口；
layout regs：显示源代码/反汇编和CPU寄存器窗口；
layout split：显示源代码和反汇编窗口；
Ctrl + L：刷新窗口；
</pre>

# 在cmake中使用GDB
 >（1）首先在CMakeLists.txt中加入
```
SET(CMAKE_BUILD_TYPE "Debug") 
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
```
 原因是CMake 中有一个变量 CMAKE_BUILD_TYPE ,可以的取值是 Debug Release RelWithDebInfo >和 MinSizeRel。
当这个变量值为 Debug 的时候，CMake 会使用变量 CMAKE_CXX_FLAGS_DEBUG 和 CMAKE_C_FLAGS_DEBUG 中的字符串作为编译选项生成 Makefile;

> （2）重新编译<br>
$  cmake  -DCMAKE_BUILD_TYPE=Debug    Path     
 注： Path 为源码的文件夹路径，如果 需要 Release 版也可以  -DCMAKE_BUILD_TYPE ＝ Release。 然后：<br>
$ cd  Path <br>
$ make<br>

>（3）进行调试<br>
$ gdb  sample<br>
注：sample 为该可执行文件
