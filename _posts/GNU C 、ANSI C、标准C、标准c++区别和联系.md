

```
---
layout: post
title: GNU C 、ANSI C、标准C、标准c++区别和联系
date:   2018-02-09  
cover: https://i.loli.net/2018/07/26/5b594a66a963b.jpg
categories: 编程
tags: C/C++
---
```



GNU计划，又称革奴计划，是由Richard Stallman在1983年9月27日公开发起的。它的目标是创建一套完全自由的操作系统。它在编写linux的时候自己制作了一个标准成为 GNU C标准。ANSI 美国国家标准协会,它对C做的标准ANSI C标准后来被国际标准协会接收成为 标准C 所以 ANSI C 和标准C是一个概念



## *ANSI C*和*标准C++*的差别

这里的ANSI C指的是最新的标准－C99

1、ANSI C不支持引用

2、ANSI C不支持函数重载

3、ANSI C多了两个整型（long long、unsigned long long），不过最新的C++编译器已经支持这两种整型

4、ANSI C不支持C++中的一个变量初始化方式，例如：int a(8);

5、ANSI C声明结构时必须使用struct关键字，而标准C++不需要

6、ANSI C标准库中的一些头文件，在标准C++中有了新的名称，例如ctime、cstring、climits、cfloat、cctype，有些文件不仅是名称上的变化

7、ANSI C不支持名称空间

8、ANSI C不包含bool类型，以及true和false关键字

9、声明函数时，参数为空的含义不同。在ANSI C中表示接受任意个数的参数，而在标准C++中表示不接受参数

10、ANSI C不支持内联函数

11、ASNI C不支持默认参数

12、ANSI C不支持可用于全局变量的作用域解析操作符（：：）

13、使用const定义的全局常量在ANSI C中具有外部链接性，在标准C++中具有内部链接性，所以在标准C++中声明外部链接性的全局常量必须使用extern，例如：extern const int a = 10;



## *GNU C*比**ANSI C*扩展的地方

### 允许零长度数组

GNU C允许零长度数组，在定义变长对象的头结构时，这个特性非常有用。

```c
struct var_data

{

      int len;

      char data[0];

};

		char data[0]仅仅意味着程序中通过var_data的结构体实例的data[index]成员可以访问len之后的第index个地址，并没有为data[0]分配内存.
   假设struct var_data的数据域保存在struct var_data紧接着的内存区域，通过如下代码可以遍历这些数据：

struct var_data s;

...

for (i=0;i<s.len;i++)

{

    printf("%02x",s.data[i]);

}
```



### case范围

```c
GNU C 支持case x...y 这样的语法，区间[x,y]的数都会满足这个case的条件

switch(c)

{

      case '0'...'9': c-='0';

      break;

      case 'a'...'f': c-='a'-10;

      break;

      case 'A'...'F': c-='A'-10;

      break;

}
```

### 语句表达式

```c++
GNU C把包含在括号里的复合语句看做是一个表达式，称为语句表达式，它可以出现在任何允许表达式的地方。我们可以在语句表达式中使用原本只能在复合语句中使用的循环变量、局部变量等，例如

#define min_t(type,x,y) /

({type __x=(x); type __y=(y);__x<__y?__x:__y})

int ia,ib,mini;

mini=min_t(int,ia,ib);

这样，因为重新定义了__x和__y这两个局部变量，所以上述方法定义的宏将不会有副作用。在标准C中，对应的宏通常会有副作用：

#define min(x,y) ((x)<(y)?(x):(y))

而代码min(++ia,++ib)将会被展开为

((++ia)<(++ib)?(++ia):(++ib)) 传入宏的参数会被增加两次。
```

### typeof关键字

```c++
typeof(x)语句可以获得x的类型，因此，我们可以借助typeof重新定义第3条提到的min_t这个宏

#define min(x,y) /

({ /

      const typeof(x) _x=(x);/

      const typeof(y) _y=(y);/

      (void) (&_x==&_y);/

       _x<_y ? _x: _y ; })

我们不需要像第三条时那样传一个type进去，因为通过typeof(x)可以得到type。

代码 (void) (&_x==&_y);的作用是检查_x和_y的类型是否一致。

```

### 可变参数的宏

```c++
标准C只支持可变参数的函数，意味着函数的参数可以是不固定的

例如printf()函数的原型是

int printf(const char *format [,argument]...)

而在GNU C中，宏也可以接受可变数目的参数，例如

#define pr_debug(fmt,arg...) printk(fmt,##arg)

这里arg表示其余的参数可以是零个或多个，这些参数以及参数之间的逗号构成arg的值，

在宏扩展时替换arg ，例如

pr_debug("%s:%d",filename,line);

被扩展为

printk("%s:%d",filename,line);

使用##的原因是为了处理arg不代表任何参数的情况，这时候，前面的逗号就变得多余了。

使用##之后，GNU C预处理器会丢弃前面的逗号，这样代码

pr_debug("success!/n") 会被正确扩展为 printk("success!/n")

而不是 printk("success!/n",);

```

### 标号元素

```c++
标准c要求数组或结构体的初始化值必须以固定的顺序出现，在GNU C中，通过指定索引或结构体成员名，允许初始化值得以任意顺序出现。

指定数组索引的方法是在初始化值前添加 [INDEX]= ，当然也可以用 [FIRST...LAST]= 的形式指定一个范围。例如下面的代码定义一个数组，并把其中的所有元素赋值为0：

unsigned char data[MAX] ={[0...MAX-1]=0 };
下面的代码借助结构体成员名初始化结构体：

struct file_operations DEMO_fops = {

    owner :    THIS_MODULE,

    llseek:      DEMO_llseek,

    read:       DEMO_read,

    write:       DEMO_write,

    ioctl:        DEMO_ioctl,

    open:        DEMO_open,

    release:   DEMO_release,

};

但是Linux 2.6还是推荐采用标准C的方式，如下

struct file_operations DEMO_fops = {

    .owner =    THIS_MODULE,

    .llseek =   DEMO_llseek,

    .read =     DEMO_read,

    .write =    DEMO_write,

    .ioctl =    DEMO_ioctl,

    .open =     DEMO_open,

    .release = DEMO_release,

};
```

### 当前函数名

```c++
GUN C预定义了两个标识符保存当前的函数名，__FUNCTION__保存函数在源码中的名字，

__PRETTY_FUNCTION__保存带语言特色的名字。在c函数中，这两个名字是相同的。
void example()

{

      printf("This is function: %s ",__FUNCTION__);

}
代码中的__FUNCTION__意味着字符串"example"
```

### 特殊属性声明

```c++
GNU C允许声明函数、变量和类型的特殊属性，以便进行手工的代码优化和定制代码检查的方法。指定一个声明的属性，只需要在申明后添加 __attribute__((ATTRIBUTE))

其中ATTRIBUTE为属性说明，如果存在多个属性，则以逗号分隔。GNU C支持noreturn format section aligned packed等十多个属性

noreturn属性作用于函数，表示该函数从不返回。这会让编译器优化代码，并消除不必要的的警告信息。例如

#define ATTRIB_NORET __attribute__ ((noreturn)) ....

asmlinkage NORET_TYPE void do_exit(long error_code) ATTRIB_NORET;

format属性也可用于函数，表示该函数printf scanf 或strftime风格的参数，指定format属性可以让编译器根据格式串检查参数类型。例如：

asmlinkage int printk(const char * fmt,...)/

__attribute__((format(printf,1,2)));

详细的可以看http://blog.163.com/sunm_lin/blog/static/9192142200741533038695/

unused属性作用于函数和变量，表示该函数或变量可能不会被用到，避免编译器产生的警告信息。

aligned属性指定结构体、变量、联合体的对齐方式。packed属性作用于变量和类型，表示压缩结构体，使用最小的内存。

struct examprl_struct

{

      char a;

      int b;

      long c;

}__attribute__((packed));

注意，这个__attribute__((packed))只能用在GNU C

```

### 内建函数

```c++
GNU C 提供了大量的内建函数，其中很多是标准 C 库函数的内建版本，例如memcpy，它们与对应的 C 库函数功能相同，本文不讨论这类函数，其他内建函数的名字通常以 __builtin 开始。

* __builtin_return_address (LEVEL)

内建函数 __builtin_return_address 返回当前函数或其调用者的返回地址，参数LEVEL 指定在栈上搜索框架的个数，0 表示当前函数的返回地址，1 表示当前函数的调用者的返回地址，依此类推。例如：

++++ kernel/sched.c

437:                 printk(KERN_ERR “schedule_timeout: wrong timeout ”

438:                        “value %lx from %p/n”, timeout,

439:                        __builtin_return_address(0));

* __builtin_constant_p(EXP)

内建函数 __builtin_constant_p 用于判断一个值是否为编译时常数，如果参数 EXP 的值是常数，函数返回 1，否则返回0。例如：

++++ include/asm-i386/bitops.h

249: #define test_bit(nr,addr) /

250: (__builtin_constant_p(nr) ? /

251: constant_test_bit((nr),(addr)) : /

252: variable_test_bit((nr),(addr)))

很多计算或操作在参数为常数时有更优化的实现，在 GNU C 中用上面的方法可以根据参数是否为常数，只编译常数版本或非常数版本，这样既不失通用性，又能在参数是常数时编译出最优化的代码。

* __builtin_expect(EXP, C)

内建函数 __builtin_expect 用于为编译器提供分支预测信息，其返回值是整数表达式 EXP 的值，C 的值必须是编译时常数。例如：

++++ include/linux/compiler.h

13: #define likely(x)       __builtin_expect((x),1)

14: #define unlikely(x)     __builtin_expect((x),0)

++++ kernel/sched.c

564:         if (unlikely(in_interrupt())) {

565:                 printk(”Scheduling in interrupt/n”);

566:                 BUG();

567:         }

这个内建函数的语义是 EXP 的预期值是 C，编译器可以根据这个信息适当地重排语句块的顺序，使程序在预期的情况下有更高的执行效率。上面的例子表示处于中断上下文是很少发生的，第 565-566 行的目标码可能会放在较远的位置，以保证经常执行的目标码更紧凑。
```




