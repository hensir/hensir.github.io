---

title: C-Primer-Puls第十一章复习题目和编程练习题的答案
date: 2020-01-28 07:24:00
tags: [答案,题目]
categories: C语言

---


本章内容为《C Primer Plus第六版》第十一章复习题和编程练习题的答案
从第十一章开始所有的c语言编程练习题答案代码格式化格式都将为
C/C++ for Visual Studio Code扩展提供的Visual Studio格式方式
扩展仓库地址：https://github.com/microsoft/vscode-cpptools
## 复习题
### 第一题
1. 下面字符串的声明有什么问题？
``` c
int main(void)
{
    char name[] = {'F', 'e', 's','s' };
    ...
}
```
<!--more-->
----------


### 第二题
2. 下面的程序会打印什么？
``` c
#include <stdio.h>
int main(void)
{
    char note[] = "See you at the snack bar.";
    char *ptr;
    ptr = note;
    puts(ptr);
    puts(++ptr);
    note[7] = '\0';
    puts(note);
    puts(++ptr);    //注意下这行
    return 0;
}
```

----------


### 第三题
3. 下面的程序会打印什么？
        #include<stdio.h>
        #include<string.h>
        int main(void)
        {
            char food[] = "Yummy";
            char *ptr;
            ptr = food + strlen(food);  //strlen()函数的返回值为int型成功记录字符的数量
            while (--ptr >= food)
                puts(ptr);
            return 0;
        }

----------


### 第四题
4. 下面的程序会打印什么？
``` c
#include <stdio.h>
#include <string.h>
int main(void)
{
    char goldwyn[40] = "art of it all ";
    char samuel[40] = "I read p";
    const char *quote = "the way through.";
    strcat(goldwyn, quote);
    strcat(samuel, goldwyn);
    puts(samuel);
    return 0;
}
```

----------



### 第五题

5. 下面的练习涉及字符串、循环、指针和递增指针。首先，假设定义了下面的函数：

        #include <stdio.h>
            char *
            pr(char *str)
        {
            char *pc;
            pc = str;
            while (*pc)
                putchar(*pc++);
            do
            {
                putchar(*--pc);
            } while (pc - str);
            return (pc);
        }
考虑下面的函数调用： x = pr("Ho Ho Ho!");
a.将打印什么？
b.x是什么类型？
c.x的值是什么？
d.表达式*--pc是什么意思？与--*pc有何不同？
e.如果用*--pc替换--*pc，会打印什么？
f.两个while循环用来测试什么？
g.如果pr()函数的参数是空字符串，会怎样？
h.必须在主调函数中做什么，才能让pr()函数正常运行？

----------


### 第六题
6. 假设有如下声明：
char sign = '$';
sign占用多少字节的内存？'$'占用多少字节的内存？"$"占用多少字节的内存？

----------


### 第七题
7. 下面的程序会打印出什么？
``` c
#include <stdio.h>
#include <string.h>
#define M1 "How are ya, sweetie? "
char M2[40] = "Beatthe clock.";
char *M3 = "chat";
int main(void)
{
    char words[80];
    printf(M1);
    puts(M1);
    puts(M2);
    puts(M2 + 1);
    strcpy(words, M2);
    strcat(words, " Win a toy.");
    puts(words);
    words[4] = '\0';
    puts(words);
    while (*M3)
        puts(M3++);
    puts(--M3);
    puts(--M3);
    M3 = M1;
    puts(M3);
    return 0;
}
```

----------


### 第八题
8. 下面的程序会打印出什么？
``` c
#include <stdio.h>
int main(void)
{
    char str1[] = "gawsie";
    char str2[] = "bletonism";
    char *ps;
    int i = 0;
    for (ps = str1; *ps != '\0'; ps++)
    {
        if (*ps == 'a' || *ps == 'e')
            putchar(*ps);
        else
            (*ps)--;
        putchar(*ps);
    }
    putchar('\n');
    while (str2[i] != '\0')
    {
        printf("%c", i % 3 ? str2[i] : '*');
        ++i;
    }
    return 0;
}
```

----------


### 第九题
9. 本章定义的s_gets()函数，用指针表示法代替数组表示法便可减少一个变量i。请改写该函数。
``` c
char *s_gets(char *st, int n)   //原型
{
    char *ret_val;
    int i = 0;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        while (st[i] != '\n' && st[i] != '\0')  //指针表示法的一大特性就是可以使用递增运算符
            i++;                                //指针加一及将数值赋给解引用后的指针
        if (st[i] == '\n')
            st[i] = '\0';
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```

----------


### 第十题
10. strlen()函数接受一个指向字符串的指针作为参数，并返回该字符串的长度。请编写一个这样的函数。
    //空格也算字符
----------


### 第十一题
11. 本章定义的s_gets()函数，可以用strchr()函数代替其中的while循环来查找换行符。请改写该函数。
    //还有另一个叫做strrchar()的函数  中间多了一个r  函数返回指定字符最后一次出现的位置
----------


### 第十二题
12. 设计一个函数，接受一个指向字符串的指针，返回指向该字符串第1个空格字符的指针，或如果未找到空格字符，则返回空指针。

----------


### 第十三题
13. 重写程序清单11.21，使用ctype.h头文件中的函数，以便无论用户选择大写还是小写，该程序都能正确识别答案。
//作者在答案里居然改了常量答案  //我的方案是全部字符串小写 然后在调用函数让第一个再大写 将这些步骤封装成函数 在s_gets函数后执行
----------

## 编程练习
### 第一题
1. 设计并测试一个函数，从输入中获取下n个字符（包括空白、制表符、换行符），把结果储存在一个数组里，它的地址被传递作为一个参数。
``` c
#include <stdio.h>
#define SIZE 20
char *getn(char *, int);
int main(void) //独立一行的^z才是EOF
{
    char str[SIZE];
    char *ch = getn(str, SIZE - 1);
    puts(str);
    puts(ch);
    return 0;
}
char *getn(char *str, int n)
{
    int i = 0;
    while (i < n)
    {
        str[i] = getchar();
        if (str[i] == EOF)
        {
            str[i] = '\0';
            return NULL;
        }
        i++;
    }
    str[i] = '\0';
    return str;
}
```
----------


### 第二题
2. 修改并编程练习1的函数，在n个字符后停止，或在读到第1个空白、制表符或换行符时停止，哪个先遇到哪个停止。不能只使用scanf()。
``` c
#include <stdio.h>
#include <ctype.h>
#define SIZE 20
char *getn(char *, int);
int main(void)
{
    char str[SIZE];
    char *ch = getn(str, SIZE - 1);
    puts(str);
    puts(ch);
    return 0;
}
char *getn(char *str, int n)
{
    int i = 0;
    while (i < n)
    {
        if ((str[i] = getchar()) == EOF || isspace(str[i]))
            break;
        else
            i++;
    }
    str[i] = '\0';
    return str;
}
```

----------


### 第三题
3. 设计并测试一个函数，从一行输入中把一个单词读入一个数组中，并丢弃输入行中的其余字符。该函数应该跳过第1个非空白字符前面的所有空白。将一个单词定义为没有空白、制表符或换行符的字符序列。
``` c
#include <stdio.h>
#include <ctype.h>
#include <stdbool.h>
char *getn(char *);
int main(void)
{
    char str[20];
    char *ch = getn(str);
    puts(str);
    puts(ch);
    return 0;
}
char *getn(char *str)
{
    int i = 0, t = 0;
    while (str[i] = getchar())
    {
        bool O = isspace(str[i]);
        if (O && t == 0)        //如果当前字符为空格 且t=0  t另有作用
            continue;           //则返回while重新接收字符 这样就保证了跳过第一个非空白字符前面的所有空白
        else if (str[i] == EOF) //
            break;
        else if (O && t == 1)   //如果当前字符为空格 且t=1则跳出循环
        {
            while(str[i] != '\n')      //这里再做一个清除工作
                str[i] = getchar();
            break;              //假如这里字符的确为空格但t不等于则说明这个空格是第一个非空白字符前面的空白
        }
        else
        {
            i++;                //如果当前字符不为空格 则将索引指向下一个元素
            t = 1;              //且t=1 用以标明已经开始接收不间断字符
        }                       //如果再遇到标准空格 那么上面那个elseif就会起作用了
    }
    str[i] = '\0';              //同样不保留换行符
    return str;
}
```
----------


### 第四题
4. 设计并测试一个函数，它类似编程练习3的描述，只不过它接受第2个参数指明可读取的最大字符数。
``` c
#include <stdio.h>
#include <ctype.h>
#include <stdbool.h>
char *getn(char *, int);
int main(void)
{
    int size;
    scanf("%d", &size);
    char str[size];             //变长数组
    char *ch = getn(str, size - 1); //最后一个位置留给空字符所以size要减一
    puts(str);
    puts(ch);
    return 0;
}
char *getn(char *str, int n)
{
    int i = 0, t = 0;
    while ((i < n) && (str[i] = getchar()))
    {
        bool O = isspace(str[i]);
        if (O && t == 0)
            continue;
        else if (str[i] == EOF)
            break;
        else if (O && t == 1)
        {
            while (str[i] != '\n')
                str[i] = getchar();
            str[i] = '\0';
            break;
        }
        else
        {
            i++;
            t = 1;
        }
    }
        str[i] = '\0';
    return str;
}
```
----------


### 第五题
5. 设计并测试一个函数，搜索第1个函数形参指定的字符串，在其中查找第2个函数形参指定的字符首次出现的位置。如果成功，该函数返指向该字符的指针，如果在字符串中未找到指定字符，则返回空指针（该函数的功能与 strchr()函数相同）。在一个完整的程序中测试该函数，使用一个循环给函数提供输入值。
``` c
#include <stdio.h>
char *findchr(char *, char);
int main(void) //假设用户是正常人
{
    char str[20];
    char ch;
    while (scanf("%s %c", str, &ch) == 2) //tips: 如果写成两个scanf那就需要清除缓冲区
    {                                     //会残留换行符
        char *pt = findchr(str, ch);
        putchar(*pt);                //pt 指向的字符
        putchar('\n');
        printf("%p", pt);            //pt 指向的字符的地址
    }
    return 0;
}
char *findchr(char *str, char ch)
{
    while (*str != '\0')
    {
        if (*str == ch)
            return str;
        else
            str++;
    }
    return NULL;
}
```
----------


### 第六题
6. 编写一个名为is_within()的函数，接受一个字符和一个指向字符串的指针作为两个函数形参。如果指定字符在字符串中，该函数返回一个非零值 （即为真）。否则，返回0（即为假）。在一个完整的程序中测试该函数， 使用一个循环给函数提供输入值。
``` c
#include <stdio.h>
char *s_gets(char *, int); //获取指定数量的字符 且将回车符替换为空字符
int is_within(char, char *);
int main(void)
{
    char ch;
    char str[20];
    while (s_gets(str, 20) && str[0] != '\0')
    {
        ch = getchar();
        printf("%d\n", is_within(ch, str));
        while (getchar() != '\n') //清空缓冲区
            continue;
    }
    return 0;
}
int is_within(char ch, char *str)
{
    while (*str)
    {
        if (*str == ch)
            return 1;
        str++;
    }
    return 0;
}
char *s_gets(char *st, int n)
{
    char *ret_val;
    int i = 0;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        while (st[i] != '\n' && st[i] != '\0')
            i++;
        if (st[i] == '\n')
            st[i] = '\0';
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```
----------


### 第七题
7. strncpy(s1, s2, n)函数把s2中的n个字符拷贝至s1中，截断s2，或者有必要的话在末尾添加空字符。如果s2的长度是n或多于n，目标字符串不能以空字符结尾。该函数返回s1。自己编写一个这样的函数，名为mystrncpy()。在一个完整的程序中测试该函数，使用一个循环给函数提供输入值。
``` c
#include <stdio.h>  //如果按照作者第二句来做会出一些混乱的错误
#include <string.h> //且第二句好像并不符合原strncpy()函数的作用
#define SIZE 20
char *mystrncpy(char *, char *, int);
char *s_gets(char *st, int n); //获取指定数量的字符 不带换行符
int main(void)
{
    char s1[SIZE];
    char s2[SIZE];
    int n;
    while (fgets(s2, SIZE, stdin) && s2[0] != '\n') //注意下不同的情况当然要做不一样的判断
    {                                               //fgets()是接收换行符的
        printf("你想复制多少个字符");
        scanf("%d", &n);
        getchar(); //去除scanf()留下的换行符
        char *funback = mystrncpy(s1, s2, n);
        printf("fb = %s\n", funback);
        printf("s1 = %s\n", s1);
        printf("请输入下一段字符串\n");
    }
    printf("done");
    return 0;
}
char *mystrncpy(char *s1, char *s2, int n)
{
    for (int i = 0; i < n; i++)
        s1[i] = s2[i];
    return s1;
}
char *s_gets(char *st, int n)
{
    char *ret_val;
    int i = 0;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        while (st[i] != '\n' && st[i] != '\0')
            i++;
        if (st[i] == '\n')
            st[i] = '\0';
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```
----------


### 第八题
8. 编写一个名为string_in()的函数，接受两个指向字符串的指针作为参数。如果第2个字符串中包含第1个字符串，该函数将返回第1个字符串开始的地址。例如，string_in("hats", "at")将返回hats中a的地址。否则，该函数返 回空指针。在一个完整的程序中测试该函数，使用一个循环给函数提供输入值。
``` c
#include <stdio.h>
#include <string.h>
char *string_in(char *, char *);
int main(void)
{
    char s1[20], s2[20];
    puts("s1");
    while (fgets(s1, 20, stdin) && s1[0] != '\n') //两个检测 不为EOF和换行符 因为fgets()函数的返回值
    {
        puts("s2");
        fgets(s2, 20, stdin);
        char **funback = string_in(s1, s2);
        printf("指针指向的字符%c\n指针指向字符的地址%X\n", *funback, funback);
        puts("s1");
    }
    puts("done");
    return 0;
}
char *string_in(char *s1, char *s2)
{
    int i, j;
    int len = strlen(s2) - 1;       //求s2最大有效值索引
    for (i = 0; s1[i] != '\0'; i++) //外层只管当前索引得值不为空字符  这样就把整个s1给遍历了一遍
    {
        char *pt = &s1[i];          //记录当前索引值
        for (j = 0; s1[i + j] == s2[j]; j++)
        {
            if (j == len)           //如果当前索引值是s2最后一个有效值
                return (char *)pt;
        }
    }
    return NULL;
}
```
----------

### 第九题
9. 编写一个函数，把字符串中的内容用其反序字符串代替。在一个完整的程序中测试该函数，使用一个循环给函数提供输入值。
``` c
#include <stdio.h>
#include <string.h>
void reversal(char *);
int main(void)
{
    char str[20];
    while (fgets(str, 20, stdin) && str[0] != '\n')
    {
        reversal(str);
        puts(str);
    }
    return 0;
}
void reversal(char *str)
{
    int i = 0;
    int len = strlen(str);      //还有搞前后temp替换的
    char temp[len + 1];
    temp[len] = '\0';
    while (len)
        temp[i++] = str[--len];
    strcpy(str, temp);
}
```
----------

### 第十题
10. 编写一个函数接受一个字符串作为参数，并删除字符串中的空格。在一个程序中测试该函数，使用循环读取输入行，直到用户输入一行空行。 该程序应该应用该函数只每个输入的字符串，并显示处理后的字符串。
``` c
#include <stdio.h>
void drop_space(char *);
int main(void)
{
    char str[20];
    while (fgets(str, 20, stdin) && str[0] != '\n' && str[0] != ' ')
    {
        drop_space(str);
        puts(str);
    }
    return 0;
}
void drop_space(char *str)
{
    int i, j;
    for (i = 0, j = 0; str[i] != '\0'; i++)     //遍历
    {
        if (str[i] != ' ')          //如果当前索引值不为空格
        {
            str[j] = str[i];        //就把当前索引值赋值给 从 0 另外计数的原指针
            if (i != j)             //这个判断说明之前遇到空格了 所以要把i的索引值变为空字符
                str[i] = '\0';      //可能会有点迷  完整的跑一边逐句吧
            j++;
        }
    }
}
```
----------

### 第十一题
11. 编写一个函数，读入10个字符串或者读到EOF时停止。该程序为用户提供一个有5个选项的菜单：打印源字符串列表、以ASCII中的顺序打印字符串、按长度递增顺序打印字符串、按字符串中第1个单词的长度打印字符串、退出。菜单可以循环显示，除非用户选择退出选项。当然，该程序要能真正完成菜单中各选项的功能。
``` c
#include <stdio.h>
#include <string.h>
#define SIZE 11
void getten(char *);          //获取十个字符
void putstr(const char *);    //打印源字符串列表
void oba(const char *);       //以ASCII中的顺序打印字符串    order by ascii
void triangle(const char *);  //按长度递增顺序打印字符串      直角三角形
void firstword(const char *); //按字符串中第1个单词的长度打印字符串 打印第一个单词
int main(void)
{
    char str[SIZE];
    char *menu = "a. 打印源字符串列表           b. 以ASCII中的顺序打印字符串\nc. 按长度递增顺序打印字符串   d. 按字符串中第1个单词的长度打印字符串\nq. 退出";
    char ch;
    getten(str);
    puts(menu);
    while ((ch = getchar()) != 'q')
    {
        while (getchar() != '\n')
            continue;
        switch (ch)
        {
        case 'a':
            putstr(str);
            break;
        case 'b':
            oba(str);
            break;
        case 'c':
            triangle(str);
            break;
        case 'd':
            firstword(str);
            break;
        default:
            printf("输入错误\n");
            puts(menu);
            break;
        }
    }
    return 0;
}
void firstword(const char *str)
{
    int i;
    for (i = 0; str[i] != ' ' && str[i] != '\0'; i++)
        putchar(str[i]);
    putchar('\n');
}
void triangle(const char *str)
{
    int i, j;
    for (i = 0; str[i] != '\0'; i++)
    {
        for (j = 0; j <= i; j++)
            putchar(str[j]);
        putchar('\n');
    }
}
void oba(const char *str)
{
    int i, j;
    char temp;                      //暂存
    char pt[SIZE];
    strncpy(pt, str, 10);           //做了一个副本
    for (i = 0; pt[i]; i++)         //cpp做过一个示例  和它一样的流程
    {
        for (j = 0; pt[j]; j++)
        {
            if (pt[i] < pt[j])
            {
                temp = pt[i];
                pt[i] = pt[j];
                pt[j] = temp;
            }
        }
    }
    puts(pt);
}
void putstr(const char *str)
{
    while (*str)
    {
        putchar(*str);
        str++;
    }
    putchar('\n');
}
void getten(char *str)
{
    int i;
    for (i = 0; i < (SIZE - 1); i++)    //数组从零计数
    {
        str[i] = getchar();
        if (str[i] == '\n' || str[i] == EOF)
        {
            str[i] = '\0';
            break;
        }
    }
    if (i == (SIZE - 1))        //如果为真，说明用户输入字符数量超过了10个或正好十个
    {                           //因为上面for的判断 所以我们只需要检测变量i就够了
        str[SIZE] = '\0';
        while (getchar() != '\n') //test
            continue;
    }
}
```
----------

### 第十二题
12. 编写一个程序，读取输入，直至读到 EOF，报告读入的单词数、大写字母数、小写字母数、标点符号数和数字字符数。使用ctype.h头文件中的函数。
``` c
#include <stdio.h>
#include <ctype.h>
int main(void)
{
    char str[30];
    int i = 0, t = 0, word = 1, upper = 0, lower = 0, punct = 0, digit = 0;
    while ((str[i] = getchar()) && str[i] != EOF) //当然这样很不安全
    {
        if (isspace(str[0]))      //如果开头是空白字符则
            continue;
        i++;
    }
    if (i != 0)
        str[i - 1] = '\0'; //这个位置是换行符 然后我把它换为空字符
    i = 0;
    while (str[i])
    {
        if (isupper(str[i]))            //依次为统计大写，小写，标点符号，数字，单词数量
            upper++;
        else if (islower(str[i]))
            lower++;
        else if (ispunct(str[i]))
            punct++;
        else if (isdigit(str[i]))
            digit++;
        if ((isspace(str[i]) && t == 1))
        {
            word++;
            i++;
        }
        else
        {
            t = 1;
            i++;
        }
    }
    printf("读入单词数有%d个\n"
           "大写字母数有%d个\n"
           "小写字母数有%d个\n"
           "标点符号数有%d个\n"
           "数字字符数有%d个\n",
           word, upper, lower, punct, digit);
    return 0;
}
```
----------

### 第十三题
13. 编写一个程序，反序显示命令行参数的单词。例如，命令行参数是see you later，该程序应打印later you see。
``` c
#include <stdio.h>
int main(int argc, char *argv[])
{
    for (int i = argc - 1; i != 0; i--) //argc记录总共有多少个字符串 因为[0]元素是内定的程序磁盘地址
        printf("%s ", argv[i]);         //这里减一 然后反向遍历这个指向数组的指针
    return 0;                           //另外双引号可以把多个单词括起来形成一个参数
}
```
----------

### 第十四题
14. 编写一个通过命令行运行的程序计算幂。第1个命令行参数是double类型的数，作为幂的底数，第2个参数是整数，作为幂的指数。
``` c
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char *argv[])
{
    int i;
    double num = atof(argv[1]);
    int exponent = atoi(argv[2]);
    double result = num;
    for (i = 1; i < exponent; i++)
        result *= num;
    if (exponent == 0)
        printf("%f", num / num);
    else
        printf("%f", result);
    return 0;
}
```
----------

### 第十五题
15. 使用字符分类函数实现atoi()函数。如果输入的字符串不是纯数字，该函数返回0。
``` c
#include <stdio.h>
#include <ctype.h>
int catoi(char *);
int main(void)
{
    char str[20];
    gets(str);
    int i = myatoi(str);
    printf("%d", i);
    return 0;
}
int myatoi(char *p)
{
    int len = strlen(p);
    int i, n = 0;
    int n = 0;
    for (i = 0; i < len; i++)
    {
        if (!isdigit(p[i]))
            return 0;
        else                           //自动转换
            n = n * 10 + (p[i] - '0'); // n =   1 * 10 + (50 - 48)
    }                                  // n =  12 * 10 + (51 - 48)
    return n;                          // n = 123 * 10 + (52 - 48)
}
```
----------

### 第十六题
16. 编写一个程序读取输入，直至读到文件结尾，然后把字符串打印出来。该程序识别和实现下面的命令行参数：
 -p  按原样打印
 -u  把输入全部转换成大写
 -l  把输入全部转换成小写
 如果没有命令行参数，则让程序像是使用了-p参数那样运行。
``` c
#include <stdio.h>
#include <ctype.h>
#include <string.h>
void getstr(char *);
int main(int argc, char *argv[])    //题外话 python语言没有switch语句
{
    char str[30] = "HELLOWORLD";
    char *pt;
    getstr(str);
    if (strcmp(argv[1], "-p") == 0)         //整个swithch语句
        puts(str);
    else if (strcmp(argv[1], "-u") == 0)    //这里没用switch是因为case后面的语句可能不支持两个字符
    {                                       //时间问题所以我没去尝试
        for (pt = str; *pt; pt++)
            *pt = toupper(*pt);
        puts(str);
    }
    else if (strcmp(argv[1], "-l") == 0)
    {
        for (pt = str; *pt; pt++)
            *pt = tolower(*pt);
        puts(str);
    }
    else
        puts(str); //这个就是default选项
    return 0;
}
void getstr(char *str)
{
    int i = 0;
    while ((str[i] = getchar()) && str[i] != EOF)
    {
        if (isspace(str[0]))
            continue;
        i++;
    }
    if (i != 0)
        str[i - 1] = '\0';
}
```
----------
