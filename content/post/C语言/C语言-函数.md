---
author: zty
title: C语言-函数
date: 2022-05-11
description:  C语言
series:
  - C语言
tags : [
    C语言基础,二级考试
]
categories : [
    编程基础
]
series : [二级考试]
aliases : [C语言基础]
---
```
函数的定义
形参和实参
调用
全局变量和局部变量
作用域
递归函数
随机数生成
```
<!--more-->
函数就是用户自定义了一串常用的代码，并以固定的格式封装成一个单独的模块，以便下一回调用，只要知道这个封装模块的名字我们就可以重复的调用它。

就像以前我们所使用的头文件中的函数也是一样，我们也是调用了它们的源文件，可以方便我们使用这个函数来运行我们的程序。

将这段代码封装成函数的过程就称为函数的定义。
# C语言无参函数的定义
无参函数就是不接受用户传递过来的数据，那么定义时也可以不带参数：
```
dataType functionName(){
    //body
}
```
 - dataType 是返回值类型，它可以是C语言中任意数据类型，例如int、float、char等。
 - functionName 是函数名，它是标识符的一种，函数名后面的`()`不能少。
 - body 是函数体，它是函数需要执行的代码，是函数的主体部分，即使只有一个语句，函数体也由`{}`包围。
 - 如果有返回值，在函数体中使用return语句返回，return 出来的数据类型要和定义函数时的遥相呼应。
 
例如：
```c
#include <stdio.h>
int sum(){
    int i, sum=0;
    for(i=1; i<=100; i++){
        sum+=i;
    }
    return sum;
}
int main(){
    int a = sum();
    printf("The sum is %d\n", a);
    return 0;
}
```
运行结果：
```
The sum is 5050
```

## 函数不能嵌套定义，main也是一个函数定义，所以要将sum放在main外面。函数必须先定义后使用，所以sum要放在main前面。
注意：main是函数定义，不是函数调用，当可执行文件加载到内存后，系统从main函数开始执行，也就是说，系统会调用我们定义的main函数。

## 无返回值类型函数
有的函数不需要返回值，或者返回值类型不确定，那么可以用void表示：
```c
void hello(){
    printf ("Hello,world \n");
    //没有返回值就不需要 return 语句
}
```
void是C语言中的关键字，表示“空类型”或“无类型”，绝大部分情况下也就意味着没有return语句。

# C语言有参数的定义
如果函数需要接收用户传递过来的数据，那么定义时就要带上参数：
```
dataType functionName( dateType1 param1, dataType2 param2……){
    //body
}
```

ateType1 param1, dataType2 param2……是参数列表。函数可以有一个参数，也可以有多个，多个参数之间由，分隔。参数本质上也是变量，定义时要指明类型和名称。与无参函数的定义相比，有参函数的定义仅仅是多了一个参数列表。

数据是通过参数之间的传递，然后将数据传递到函数中进行处理，处理完成后再通过返回值返回函数外部。

函数定义时给出的参数称为形参参数，简称形参；函数调用时给出的参数称为实参参数，简称实参，函数调用时将实参中的值传递给形参，相当于一次赋值操作，但是形参中的值不能传递给实参。

## 形参和实参的区别和联系
1. 形参变量只有在调用的时候才会分配内存，调用结束后就会释放掉内存，所以形参变量只在函数内部有用。
2. 实参可以在传递之前是任何的值是变量、表达式、函数等等，但是当函数进行调用时，传输的值一定是一个确定的值。
3. 实参和形参在数量上、类型上、顺序上都必须严格一致，否则会发生“类型不匹配”的错误，当然如果能触发自动类型转换，或者进行了强制类型转换，那么实参也可以不同于形参的类型
4. 函数的调用关系是单向的，只能由实参传给形参不能由形参反向传给实参。所以在函数调用的过程中形参中的值影响不到实参。
5. 形参和实参虽然可以同名但是他们之间是相互独立的，互不影响，因为实参在函数外部有效，而形参只有在函数内部才有效。

# 函数不能嵌套定义
C语言中不允许函数嵌套定义；也就是说在一个函数内部不能定义另一个函数，函数的定义只能存在于所有函数外定义

# 函数的返回值
函数的返回值是指函数在被调用后，执行函数中的代码，所得到的结果，将这个结果通过return返回。
```
return 表达式;
```
1. 没有返回值的函数为空类型，用void表示：
```c
void func(){
    printf("https://tianlangz.top");
}
```
一旦函数的返回值类型被确定为void，就不能在接受它的值了。为了使程序有良好的可读性减少出错，凡不要求返回值的函数都应定义为void类型。

2. return语句可以有多个，可以出现在函数体的任意位置，但是每次调用函数只能有一个return语句被执行，也就是说，当在函数中执行过一个return后就会结束函数，不会再继续执行语句了，return语句还有强制结束函数执行的作用。

return语句是提前结束函数的唯一办法，return 后面可以跟一份数据，可以跟表达式，也可以跟变量，也可以跟一个数。也就是说当return后不跟任何数据时，表示什么也不返回，仅仅结束函数。

# 函数的调用
所谓函数调用，就是将一段已经写好的函数，利用函数调用使用这段函数：
```
functionName(param1, param2, param3 ...);
```

functionName 是函数名称，param1, param2, param3 ...是实参列表。实参可以是常数、变量、表达式等，多个实参用逗号,分隔。

```
//函数作为表达式中的一项出现在表达式中
z = max(x, y);
m = n + max(x, y);
//函数作为一个单独的语句
printf("%d", a);
scanf("%d", &b);
//函数作为调用另一个函数时的实参
printf( "%d", max(x, y) );
total( max(x, y), min(m, n) );
```

函数不能嵌套定义，但是能够嵌套调用：
```c
#include <stdio.h>
//求阶乘
long factorial(int n){
    int i;
    long result=1;
    for(i=1; i<=n; i++){
        result *= i;
    }
    return result;
}
// 求累加的和
long sum(long n){
    int i;
    long result = 0;
    for(i=1; i<=n; i++){
        //在定义过程中出现嵌套调用
        result += factorial(i);
    }
    return result;
}
int main(){
    printf("1!+2!+...+9!+10! = %ld\n", sum(10));  //在调用过程中出现嵌套调用
    return 0;
}
```
运行结果：1!+2!+...+9!+10! = 4037913

如果一个函数在定义或调用的过程中出现了对另一个函数的调用，则我们就称它为`主调函数`或者`主函数`，而他调用的那个函数称为`被调函数`。

当主调函数遇到被调函数是，主调函数会被暂停，会先执行调用的被调函数，被调函数处理完了，就会将主调函数继续执行下去。

而C语言的执行过程就是在多个函数中相互调用的过程，他们之间的相互调用形成的链条，这个链条的起点时main()函数，终点也是main()函数。当他调用完所有函数后会返回一个值，从而结束整个程序。

在函数的调用过程中我们也可以不直接把函数原型写在主函数前，也可以将它写在主函数后，这样我们就会用到声明，也就是你要告诉编译器我要使用这个函数，你现在没找到它不要紧，不要报错你会在程序整个执行完之前找到它，有了函数声明，你就可以将你的函数写在任何你想的位置上。
```c
#include <stdio.h>
//函数声明
int sum(int m, int n);  //也可以写作int sum(int, int);
int main(){
    int begin = 5, end = 86;
    int result = sum(begin, end);
    printf("The sum from %d to %d is %d\n", begin, end, result);
    return 0;
}
//函数定义
int sum(int m, int n){
    int i, sum=0;
    for(i=m; i<=n; i++){
        sum+=i;
    }
    return sum;
}
```

所有的头文件也是类似的编写方式，用一些特殊的办法引用声明，你才能使用这些函数

# 局部变量，和全局变量
变量的作用域由变量的定义位置决定，在不同位置定义的变量。它的作用域是不一样的。
## 局部变量
简单的来说，定义在函数内部的就称为局部变量，它的作用域只在自己函数内部，离开函数就无用了，在函数外再使用它就会报错。
1. 在main函数中定义的变量也是局部变量，只能在函数中使用。main函数和其他函数一样，地位是平等的
2. 形参变量，在函数体内定义的变量都叫局部变量，实参给形参传值的过程也就是给局部变量赋值的过程。
3. 可以在不同的函数中使用相同的变量名，他们表示不同的数据，分配不同的内存，互不干扰，也不会发生混淆。
4. 在语句块中也可以定义变量，它的作用域只限于当前语句块。
## 全局变量
在函数外定义的变量就称为全局变量，它默认作用域为整个程序，也就是.c.h文件也会受他影响。在全局变量前加上static关键字就相当于它的作用域只限于本文件，在其他文件中就无效了。
```c
int a, b;  //全局变量
void func1(){
    //TODO:
}
float x,y;  //全局变量
int func2(){
    //TODO:
}
int main(){
    //TODO:
    return 0;
}
```
a、b、x、y 都是在函数外部定义的全局变量。C语言代码是从前往后依次执行的，由于 x、y 定义在函数 func1() 之后，所以在 func1() 内无效；而 a、b 定义在源程序的开头，所以在 func1()、func2() 和 main() 内都有效。

```c
#include <stdio.h>
int n = 10;  //全局变量
void func1(){
    int n = 20;  //局部变量
    printf("func1 n: %d\n", n);
}
void func2(int n){
    printf("func2 n: %d\n", n);
}
void func3(){
    printf("func3 n: %d\n", n);
}
int main(){
    int n = 30;  //局部变量
    func1();
    func2(n);
    func3();
    //代码块由{}包围
    {
        int n = 40;  //局部变量
        printf("block n: %d\n", n);
    }
    printf("main n: %d\n", n);
    return 0;
}
```
```
运行结果：
func1 n: 20
func2 n: 30
func3 n: 10
block n: 40
main n: 30
```
代码中虽然定义了多个同名变量 n，但它们的作用域不同，在内存中的位置（地址）也不同，所以是相互独立的变量，互不影响，不会产生重复定义（Redefinition）错误。

1) 对于 func1()，输出结果为 20，显然使用的是函数内部的 n，而不是外部的 n；func2() 也是相同的情况。

当全局变量和局部变量同名时，在局部范围内全局变量被“屏蔽”，不再起作用。或者说，变量的使用遵循就近原则，如果在当前作用域中存在同名变量，就不会向更大的作用域中去寻找变量。

2) func3() 输出 10，使用的是全局变量，因为在 func3() 函数中不存在局部变量 n，所以编译器只能到函数外部，也就是全局作用域中去寻找变量 n。

3) 由{}包围的代码块也拥有独立的作用域，printf() 使用它自己内部的变量 n，输出 40。

4) C语言规定，只能从小的作用域向大的作用域中去寻找变量，而不能反过来，使用更小的作用域中的变量。对于 main() 函数，即使代码块中的 n 离输出语句更近，但它仍然会使用 main() 函数开头定义的 n，所以输出结果是 30。

`在一个函数内部修改全局变量后，它修改后的值会影响到其他函数，他在被修改后并不会自动回复，他会一直保留该值，直到下次修改。`
全局变量也是变量，他被修改后原来的数据就被洗掉了。

## 关于变量的命名
C语言规定在同一个作用域内不能出现两个相同名字的变量，否则会产生命名冲突；但是在不同的作用域内时，允许出现名字相同的变量，他们的作用域不同，彼此之间不会产生冲突

## 作用域
每个C程序都包含了多个作用域，不同的作用域可以出现同名的变量，C语言会按照从小到大的顺序去检查，一层一层去父级变量中查找变量，如果在最顶层的全局作用域中还没找到就会报错。

# 递归函数
递归调用就是一个函数在自己的函数体内调用自身称之为递归调用，这种函数称之为递归函数。
就是求阶乘：利用函数求阶乘
```c
#include <stdio.h>
long nb(int a)
{
    if(a==0 || a==1)
        return 1;
    else 
        return nb(a-1)*a;
}
int main()
{
    int a;
    scanf("%d",&a);
    printf("%d! = %d",a,nb(a));
    return 0;
}
```
我们那5！来解释一下我的程序：

|层次/层数	|调用形式|	需要计算的表达式|	从内层递归得到的结果（内层函数的返回值）|	表达式的值（当次调用的结果）|
|-|-|-|-|-|
|5|	factorial(1)|	1|	无|	1|
|4|	factorial(2)|	factorial(1) * 2|	factorial(1) 的返回值，也就是 1|	2|
|3|	factorial(3)|	factorial(2) * 3|	factorial(2) 的返回值，也就是 2|	6|
|2|	factorial(4)|	factorial(3) * 4|	factorial(3) 的返回值，也就是 6|	24|
|1|	factorial(5)|	factorial(4) * 5|	factorial(4) 的返回值，也就是 24|	120|

每一个递归调用都应该经历有限次的调用，否则会陷入无限的循环，而想让递归逐层进入在逐层退出需要：
 - 存在限制条件，也就是循环所说的边界条件，但递归不同于循环，当符合这个条件时便不再递归，当它不再继续往下递归后就会一点点逐层退出，得到你想要的值。
 - 还有你要保证每次递归调用后都会越来越接近你的那个限制条件，才能保证最后它会返回。

 # 随机数生成
 ```
 int rand (void);
 ```
 void表示不需要传递参数。

 rand()会随机生成一个位于0~RAND_MAX之间的整数。

RAND_MAX是<stdlib.h>头文件中的一个宏，它用来指明rand()所能返回的最大值。C语言标准把那个没有规定它到底是多大，只是规定它的数值至少是32767。
下面是一个随机数生成的实例：
```c
#include <stdio.h>
#include <stdlib.h>
int main(){
    int a = rand();
    printf("%d\n",a);
    return 0;
}
```
运行结果举例：193

## 随机数的本质
多次执行上面的程序你就会发现，它的数字并不会改变，实际上rand()函数产生的随机数是伪随机数，是根据一个数值按照某个公式推算出来的，这个数值我们称之为”种子“。种子在每次启动计算机时是随机的但是当启动之后种子的值就不会发生改变了，所以开机后生成的随机数也就是固定的了。

## srand()
这样我们就会用到srand函数，利用它重新来播种，这样就会发生改变。
```
srand(unsigned int seed);
```
在实际开发中，我们可以用时间作为参数，只要每次播种的时间不同，那么生成的种子也就不同，最终的数也就不一样了。

但是需要使用到<time.h>头文件中的time()函数即可得到当前时间精确到秒：
```c
srand((unsigned)time(NULL));
```

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
int main() {
    int a;
    srand((unsigned)time(NULL));
    a = rand();
    printf("%d\n", a);
    return 0;
}
```
多次运行程序，会发现每次生成的随机数都不一样了。但是，这些随机数会有逐渐增大或者逐渐减小的趋势，这是因为我们以时间为种子，时间是逐渐增大的，结合上面的正态分布图，很容易推断出随机数也会逐渐增大或者减小。

## 生成一定范围内的随机数
在实际开发中，我们往往需要一定范围内的随机数，过大或者过小都不符合要求，那么，如何产生一定范围的随机数呢？我们可以利用取模的方法：
```c
int a = rand() % 10;    //产生0~9的随机数，注意10会被整除
```
如果要规定上下限：
```c
int a = rand() % 51 + 13;    //产生13~63的随机数
```
分析：取模即取余，rand()%51+13我们可以看成两部分：rand()%51是产生 0~50 的随机数，后面+13保证 a 最小只能是 13，最大就是 50+13=63。

最后给出产生 13~63 范围内随机数的完整代码：
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
int main(){
    int a;
    srand((unsigned)time(NULL));
    a = rand() % 51 + 13;
    printf("%d\n",a);
    return 0;
}
```
























