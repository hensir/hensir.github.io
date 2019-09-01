---

title: C-Primer-Puls第四章复习题及编程练习
date: 2019-08-31 11:00:00
tags: [题目]
categories: C语言

---


本章内容为《C Primer Plus第六版》第四章复习题和编程练习题


## 复习题

### 第一题
1. 再次运行程序清单 4.1，但是在要求输入名时，请输入名和姓（根据英文书写习惯，名和姓中间有一个空格），看看会发生什么情况？为什么？
程序清单4.1：
``` c
#include <stdio.h>
#include <string.h>     // 提供strlen()函数的原型
#define DENSITY 62.4    // 人体密度（单位：磅/立方英尺）
int main()
{
    float weight, volume;
    int size, letters;
    char name[40];      // name是一个可容纳40个字符的数组
    printf("Hi! What's your first name?\n");
    scanf("%s", name);
    printf("%s, what's your weight in pounds?\n", name);
    scanf("%f", &weight);
    size = sizeof name;
    letters = strlen(name);
    volume = weight / DENSITY;
    printf("Well, %s, your volume is %2.2f cubic feet.\n", name, volume);
    printf("Also, your first name has %d letters,\n", letters);
    printf("and we have %d bytes to store it.\n", size);
    return 0;
}
```

<!--more-->

----------

### 第二题
2. 假设下列示例都是完整程序中的一部分，它们打印的结果分别是什么？
``` c
a.printf("He sold the painting for $%2.2f.\n", 2.345e2);
b.printf("%c%c%c\n", 'H', 105, '\41');
c.#define Q "His Hamlet was funny without being vulgar."printf("%s\nhas %dcharacters.\n", Q, strlen(Q));
d.printf("Is %2.2e the same as %2.2f?\n", 1201.0, 1201.0);

```


----------



### 第三题
3. 在第2题的c中，要输出包含双引号的字符串Q，应如何修改？

----------


### 第四题
4. 找出下面程序中的错误。
``` c
define B booboo
define X 10
main(int)
{
    int age;
    char name;
    printf("Please enter your first name.");
    scanf("%s", name);
    printf("All right, %c, what's your age?\n", name);
    scanf("%f", age);
    xp = age + X;
    printf("That's a %s! You must be at least %d.\n", B, xp);
    rerun 0;
}
```

----------


### 第五题
5. 假设一个程序的开头是这样：

        #define BOOK "War and Peace"
        int main(void)
        {
            float cost =12.99;
            float percent = 80.0;
请构造一个使用BOOK、cost和percent的printf()语句，打印以下内容：
        This copy of "War and Peace" sells for $12.99.
        That is 80% of list.

----------


### 第六题
6. 打印下列各项内容要分别使用什么转换说明？
a.一个字段宽度与位数相同的十进制整数
b.一个形如8A、字段宽度为4的十六进制整数
c.一个形如232.346、字段宽度为10的浮点数
d.一个形如2.33e+002、字段宽度为12的浮点数
e.一个字段宽度为30、左对齐的字符串

----------


### 第七题
7. 打印下面各项内容要分别使用什么转换说明？
a.字段宽度为15的unsigned long类型的整数
b.一个形如0x8a、字段宽度为4的十六进制整数
c.一个形如2.33E+02、字段宽度为12、左对齐的浮点数
d.一个形如+232.346、字段宽度为10的浮点数
e.一个字段宽度为8的字符串的前8个字符

----------


### 第八题
8. 打印下面各项内容要分别使用什么转换说明？
a.一个字段宽度为6、最少有4位数字的十进制整数
b.一个在参数列表中给定字段宽度的八进制整数
c.一个字段宽度为2的字符
d.一个形如+3.13、字段宽度等于数字中字符数的浮点数
e.一个字段宽度为7、左对齐字符串中的前5个字符

----------


### 第九题
9. 分别写出读取下列各输入行的scanf()语句，并声明语句中用到变量和数组。
a.101
b.22.32 8.34E−09
c.linguini
d.catch 22 e.catch 22 （但是跳过catch）

----------


### 第十题
10. 什么是空白？

----------


### 第十一题
11. 下面的语句有什么问题？如何修正？
        printf("The double type is %z bytes..\n", sizeof(double));

----------


### 第十二题
12. 假设要在程序中用圆括号代替花括号，以下方法是否可行？

        #define ( {
        #define ) }


----------




## 编程练习

### 第一题
1. 编写一个程序，提示用户输入名和姓，然后以“名,姓”的格式打印出来。

----------


### 第二题
2. 编写一个程序，提示用户输入名和姓，并执行一下操作：
a.打印名和姓，包括双引号；
b.在宽度为20的字段右端打印名和姓，包括双引号；
c.在宽度为20的字段左端打印名和姓，包括双引号；
d.在比姓名宽度宽3的字段中打印名和姓。

----------


### 第三题
3. 编写一个程序，读取一个浮点数，首先以小数点记数法打印，然后以指数记数法打印。用下面的格式进行输出（系统不同，指数记数法显示的位 数可能不同）：
a.输入21.3或2.1e+001；
b.输入+21.290或2.129E+001；

----------


### 第四题
4. 编写一个程序，提示用户输入身高（单位：英寸）和姓名，然后以下面的格式显示用户刚输入的信息：
Dabney, you are 6.208 feet tall
使用float类型，并用/作为除号。如果你愿意，可以要求用户以厘米为单位输入身高，并以米为单位显示出来。

----------


### 第五题
5. 编写一个程序，提示用户输入以兆位每秒（Mb/s）为单位的下载速度和以兆字节（MB）为单位的文件大小。程序中应计算文件的下载时间。注 意，这里1字节等于8位。使用float类型，并用/作为除号。该程序要以下面 的格式打印 3 个变量的值（下载速度、文件大小和下载时间），显示小数点后面两位数字： At 18.12 megabits per second, a file of 2.20 megabytes downloads in 0.97 seconds.

----------


### 第六题
6. 编写一个程序，先提示用户输入名，然后提示用户输入姓。在一行打印用户输入的名和姓，下一行分别打印名和姓的字母数。字母数要与相应名和姓的结尾对齐，如下所示：
        Melissa  Honeybee
              7         8
接下来，再打印相同的信息，但是字母个数与相应名和姓的开头对齐，如下所示：
        Melissa  Honeybee
        7        8

----------


### 第七题
7. 编写一个程序，将一个double类型的变量设置为1.0/3.0，一个float类型的变量设置为1.0/3.0。分别显示两次计算的结果各3次：一次显示小数点 后面6位数字；一次显示小数点后面12位数字；一次显示小数点后面16位数 字。程序中要包含float.h头文件，并显示FLT_DIG和DBL_DIG的值。1.0/3.0 的值与这些值一致吗？

----------


### 第八题
8. 编写一个程序，提示用户输入旅行的里程和消耗的汽油量。然后计算并显示消耗每加仑汽油行驶的英里数，显示小数点后面一位数字。接下来， 使用1加仑大约3.785升，1英里大约为1.609千米，把单位是英里/加仑的值转 换为升/100公里（欧洲通用的燃料消耗表示法），并显示结果，显示小数点 后面 1 位数字。注意，美国采用的方案测量消耗单位燃料的行程（值越大越 好），而欧洲则采用单位距离消耗的燃料测量方案（值越低越好）。使用 #define 创建符号常量或使用 const 限定符创建变量来表示两个转换系数。