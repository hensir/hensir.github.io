---

title: C-Primer-Puls第十四章复习题目和编程练习题的答案
date: 2020-04-08 11:02:00
tags: [答案,题目]
categories: C语言
cover: /img/c.png
---

本章内容为《C Primer Plus第六版》第十四章复习题和编程练习题的答案
## 复习题
### 第一题
1. 下面的结构模板有什么问题：
        structure
        {
            char itable;
            int num[20];
            char *togs
        }
<!--more-->

----------

### 第二题
2. 下面是程序的一部分，输出是什么？
``` c
#include <stdio.h>
struct house
{
    float sqft;
    int rooms;
    int stories;
    char address[40];
};
int main(void)
{
    struct house fruzt = {1560.0, 6, 1, "22 Spiffo Road"};
    struct house *sign;
    sign = &fruzt;
    printf("%d %d\n", fruzt.rooms, sign->stories);
    printf("%s \n", fruzt.address);
    printf("%c %c\n", sign->address[3], fruzt.address[4]);
    return 0;
}
```

----------

### 第三题
3. 设计一个结构模板储存一个月份名、该月份名的3个字母缩写、该月的天数以及月份号。

----------

### 第四题
4. 定义一个数组，内含12个结构（第3题的结构类型）并初始化为一个年份（非闰年）。

----------

### 第五题
5. 编写一个函数，用户提供月份号，该函数就返回一年中到该月为止（包括该月）的总天数。假设在所有函数的外部声明了第3题的结构模版和一个该类型结构的数组。

----------

### 第六题
6. a.假设有下面的 typedef，声明一个内含10个指定结构的数组。然后，单独给成员赋值（或等价字符串），使第3个元素表示一个焦距长度有 500mm，孔径为f/2.0的Remarkata镜头。
        typedef struct lens /* 描述镜头  */
        {
            float foclen;   /* 焦距长度，单位为mm */
            float fstop;    /* 孔径 */
            char brand[30]; /* 品牌名称 */
        } LENS;
b.重写a，在声明中使用一个待指定初始化器的初始化列表，而不是对每个成员单独赋值。

----------

### 第七题
7. 考虑下面程序片段：
``` c
        struct name
        {
            char first[20];
            char last[20];
        };
        struct bem
        {
            int limbs;
            struct name title;
            char type[30];
        };
        struct bem *pb;
        struct bem deb = {6, {"Berbnazel", "Gwolkapwolk"}, "Arcturan"};
        pb = &deb;
```
 a.下面的语句分别打印什么？
        printf("%d\n", deb.limbs);
        printf("%s\n", pb->type);
        printf("%s\n", pb->type + 2);
 b.如何用结构表示法（两种方法）表示 "Gwolkapwolk"？
 c.编写一个函数，以bem结构的地址作为参数，并以下面的形式输出结构的内容（假定结构模板在一个名为starfolk.h的头文件中）：
 Berbnazel Gwolkapwolk is a 6 -limbed Arcturan.

----------

### 第八题
8. 考虑下面的声明：
``` c
        struct fullname
        {
            char fname[20];
            char lname[20];
        };
        struct bard
        {
            struct fullname name;
            int born;
            int died;
        };
        struct bard willie;
        struct bard *pt = &willie;
```
 a. 用willie标识符标识willie结构的born成员。
 b. 用pt标识符标识willie结构的born成员。
 c. 调用scanf() 读入一个用willie标识符标识的born成员的值。
 d. 调用scanf() 读入一个用pt标识符标识的born成员的值。
 e. 调用scanf() 读入一个用willie标识符标识的name成员中lname成员的值。
 f. 调用scanf() 读入一个用pt标识符标识的name成员中lname成员的值。
 g. 构造一个标识符，标识willie结构变量所表示的姓名中名的第3个字母（英文的名在前）。
 h. 构造一个表达式，表示willie结构变量所表示的名和姓中的字母总数。

----------

### 第九题
9. 定义一个结构模板以储存这些项：汽车名、马力、EPA（美国环保局）城市交通MPG（每加仑燃料行驶的英里数）评级、轴距和出厂年份。 使用car作为该模版的标记。

----------

### 第十题
10. 假设有如下结构：
        struct gas
        {
            float distance;
            float gals;
            float mpg;
        };
a. 设计一个函数，接受struct gas类型的参数。假设传入的结构包含distance和gals信息。该函数为mpg成员计算正确的值，并把值返回该结构。
b. 设计一个函数，接受struct gas类型的参数。假设传入的结构包含distance和gals信息。该函数为mpg成员计算正确的值，并把该值赋给合适的成员。
----------

### 第十一题
11. 声明一个标记为choices的枚举，把枚举常量no、yes和maybe分别设置为0、1、2。

----------

### 第十二题
12. 声明一个指向函数的指针，该函数返回指向char的指针，接受一个指向char的指针和一个char类型的值。

----------

### 第十三题
13. 声明4个函数，并初始化一个指向这些函数的指针数组。每个函数都接受两个double类型的参数，返回double类型的值。另外，用两种方法使用该数组调用带10.0和2.5实参的第2个函数。




----------

## 编程练习
### 第一题
1. 重新编写复习题 5，用月份名的拼写代替月份号（别忘了使用strcmp()）。在一个简单的程序中测试该函数。
``` c
#include <stdio.h>
#include <string.h>
struct month
{
    char name[10];
    char abbrev[4];
    int days;
    int monumb;
};
struct month months[12] = {
    {"January", "jan", 31, 1},
    {"February", "feb", 28, 2},
    {"March", "mar", 31, 3},
    {"April", "apr", 30, 4},
    {"May", "may", 31, 5},
    {"June", "jun", 30, 6},
    {"July", "jul", 31, 7},
    {"August", "aug", 31, 8},
    {"September", "sep", 30, 9},
    {"October", "oct", 31, 10},
    {"November", "nov", 30, 11},
    {"December", "dec", 31, 12}};
char *s_gets(char *st, int n);
int days(char *);
int main(void)
{
    char abb[10];
    s_gets(abb, 10);
    printf("天数为%d", days(abb));
    return 0;
}
int days(char *pt)
{
    extern struct month months[];
    int total = 0, i;
    for (i = 0; i < 12; i++)     // 遍历对比一遍
    {
        if (strcmp(pt, months[i].abbrev) == 0)
            break;
    }
    for (int j = 0; j <= i; j++)
        total += months[j].days;
    return total;
}
char *s_gets(char *st, int n)
{
    char *ret_val;
    char *find;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        find = strchr(st, '\n'); // 查找换行符
        if (find)                // 如果地址不是NULL，
            *find = '\0';        // 在此处放置一个空字符
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```
----------

### 第二题
2. 编写一个函数，提示用户输入日、月和年。月份可以是月份号、月份名或月份名缩写。然后该程序应返回一年中到用户指定日子（包括这一天） 的总天数。
``` c
#include <stdio.h>
#include <string.h> // 平年检测 年月日数据正确检测 年月日超数检测 月全称小写缩写小写
struct months
{
    char name[10];
    char abbrev[4];
    int days;
    char monumb; // 月份号使用字符表示
};
const struct months year[12] = {
    {"January", "jan", 31, '1'},
    {"February", "feb", 28, '2'},
    {"March", "mar", 31, '3'},
    {"April", "apr", 30, '4'},
    {"May", "may", 31, '5'},
    {"June", "jun", 30, '6'},
    {"July", "jul", 31, '7'},
    {"August", "aug", 31, '8'},
    {"September", "sep", 30, '9'},
    {"October", "oct", 31, '10'},
    {"November", "nov", 30, '11'},
    {"December", "dec", 31, '12'}};
char *s_gets(char *st, int n);
int days(char *, int);
int main(void)
{
    int years, day;
    char month[10]; // 月份号 月份缩写 月份全称全代
    printf("请输入年\n");
    scanf("%d", &years);
    getchar();
    printf("请输入月\n");
    s_gets(month, 10);
    printf("请输入日\n");
    scanf("%d", &day);
    printf("在%d平年里从1月1日到%c月%d日总共有%d天", years, *month, day, days(month, day));
    return 0;
}
int days(char *pt, int day)
{
    extern const struct months year[];
    int i, total = 0;
    for (i = 0; i < 12; i++) // abbrev || name || monumb
    {
        if ((strcmp(pt, year[i].abbrev) == 0) || (strcmp(pt, year[i].name) == 0) || ((*pt) == year[i].monumb))
            break;
    }
    for (int j = 0; j < i; j++)
        total += year[j].days;
    *pt = year[i].monumb;   // 好看
    return total + day; // 加到这个月的前一个月 然后加上传过来的这个day值
}
char *s_gets(char *st, int n)
{
    char *ret_val;
    char *find;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        find = strchr(st, '\n'); // 查找换行符
        if (find)                // 如果地址不是NULL，
            *find = '\0';        // 在此处放置一个空字符
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```
----------

### 第三题
3. 修改程序清单 14.2 中的图书目录程序，使其按照输入图书的顺序输出图书的信息，然后按照标题字母的声明输出图书的信息，最后按照价格的升序输出图书的信息。
``` c
#include <stdio.h>
#include <string.h>
char *s_gets(char *st, int n);
#define MAXTITL 40
#define MAXAUTL 40
#define MAXBKS 100 /* 书籍的最大数量 */
static struct book // 作者说 栈可能不够存储这个100个这个结构的 所以使用static可以把它们存储在堆里 但我的pc可以放到栈里
{                  /* 简历 book 模板 */
    char title[MAXTITL];
    char author[MAXAUTL];
    float value;
};
int main(void) // 按照title首字母顺序打印 从a-z    然后是价格从低到高的升序打印    两个冒泡 一个字符 一个数值
{
    struct book library[MAXBKS]; /* book 类型结构的数组 */
    int index, count = 0;
    struct book temp;
    printf("Please enter the book title.\n");
    printf("Press [enter] at the start of a line to stop.\n");
    while (count < MAXBKS && s_gets(library[count].title, MAXTITL) != NULL && library[count].title[0] != '\0')
    {
        printf("Now enter the author.\n");
        s_gets(library[count].author, MAXAUTL);
        printf("Now enter the value.\n");
        scanf("%f", &library[count++].value);
        while (getchar() != '\n')
            continue;       /* 清理输入行*/
        if (count < MAXBKS) // 检测是否超过数组大小  s_gets函数不返回NULL   接收的第一个标题的元素不为空字符
            printf("Enter the next title.\n");
    }
    if (count > 0)
    {
        printf("Here is the list of your books:\n");
        for (index = 0; index < count; index++)
            printf("%s by %s: $%.2f\n", library[index].title, library[index].author, library[index].value);

        // 按title的字母升序打印
        for (index = 0; index < count; index++)
        {
            for (int j = index; j < count; j++)
            {
                if (strcmp(library[index].title, library[j].title) > 0)
                {
                    temp = library[index];
                    library[index] = library[j];
                    library[j] = temp;
                }
            }
        }
        puts("按title的字母升序打印");
        for (index = 0; index < count; index++)
        {
            printf("%s by %s: $%.2f\n", library[index].title, library[index].author, library[index].value);
        }
        // 按价格的升序打印
        for (index = 0; index < count; index++)
        {
            for (int j = index; j < count; j++)
            {
                if (library[index].value > library[j].value)
                {
                    temp = library[index];
                    library[index] = library[j];
                    library[j] = temp;
                }
            }
        }
        puts("按价格的升序打印");
        for (index = 0; index < count; index++)
        {
            printf("%s by %s: $%.2f\n", library[index].title, library[index].author, library[index].value);
        }
    }
    else
        printf("No books? Too bad.\n");
    return 0;
}
char *s_gets(char *st, int n)
{
    char *ret_val;
    char *find;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        find = strchr(st, '\n'); // 查找换行符
        if (find)                // 如果地址不是NULL，
            *find = '\0';        // 在此处放置一个空字符
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```
----------

### 第四题
4. 编写一个程序，创建一个有两个成员的结构模板：
a.第1个成员是社会保险号，第2个成员是一个有3个成员的结构，第1个成员代表名，第2个成员代表中间名，第3个成员表示姓。创建并初始化一个内含5个该类型结构的数组。该程序以下面的格式打印数据：
Dribble, Flossie M.–– 302039823
如果有中间名，只打印它的第1个字母，后面加一个点（.）；如果没有中间名，则不用打印点。编写一个程序进行打印，把结构数组传递给这个函数。
b.修改a部分，传递结构的值而不是结构的地址。
``` c
#include <stdio.h>
struct name // 非匿名结构
{
    char fname[10];
    char mname[10];
    char lname[10];
};
struct person
{
    unsigned long id;
    struct name names;
};
void a_print(struct person *);
void a_print_2(struct person *);
void b_print(struct person);
#define K 5
int main(void)
{
    struct person shebao[K] = {
        {3124567, "san", "", "zhang"},
        {3124568, "gang", "de", "guo"},
        {3124569, "peng", "yun", "yue"},
        {3124570, "si", "", "li"},
        {3124571, "wick", "", "John"}};
    printf("a-指针转数组表示法\n"); // 很明显在2020年结构的表示法同样也有指针和数组表示法
    a_print(shebao);              //  而结构指针表示法同样和数组指针表示法一样可以转换为数组表示法
    printf("a-指针表示法\n");       // 看a1为原指针转数组  和 a2指针   b2数组就不写了
    a_print_2(shebao);
    printf("b-数组表示法 传递结构的值\n");    // 这个是把结构本身给传过去了  也就是数组的元素
    for (int i = 0; i < K; i++)             // 我理解的值 是把结构中的值给一个一个声明然后传递
        b_print(shebao[i]);
    return 0;
}
void a_print(struct person *shebao)
{
    int i;
    for (i = 0; i < K; i++)
    {
        if ((shebao[i].names.mname[0]) != '\0') // 如果有中间名 打印一个中间名然后加点
            printf("%10s,%10s %c.-- %8ld\n", shebao[i].names.lname, shebao[i].names.fname, shebao[i].names.mname[0], shebao[i].id);
        else
            printf("%10s,%10s   -- %8ld\n", shebao[i].names.lname, shebao[i].names.fname, shebao[i].id);
    }
}
void a_print_2(struct person *shebao)
{
    int i;
    for (i = 0; i < K; i++, shebao++)
    {
        if ((shebao->names.mname[0]) != '\0') // 如果有中间名 打印一个中间名然后加点
            printf("%10s,%10s %c.-- %8ld\n", shebao->names.lname, shebao->names.fname, shebao->names.mname[0], shebao->id);
        else
            printf("%10s,%10s   -- %8ld\n", shebao->names.lname, shebao->names.fname, shebao->id);
    }
}
void b_print(struct person ta)
{
    if ((ta.names.mname[0]) != '\0') // 如果有中间名 打印一个中间名然后加点
        printf("%10s,%10s %c.-- %8ld\n", ta.names.lname, ta.names.fname, ta.names.mname[0], ta.id);
    else
        printf("%10s,%10s   -- %8ld\n", ta.names.lname, ta.names.fname, ta.id);
}
```

----------

### 第五题
5. 编写一个程序满足下面的要求。
a. 外部定义一个有两个成员的结构模板name：一个字符串储存名，一个字符串储存姓。
b. 外部定义一个有3个成员的结构模板student：一个name类型的结构，一个grade数组储存3个浮点型分数，一个变量储存3个分数平均数。
c. 在main()函数中声明一个内含CSIZE（CSIZE = 4）个student类型结构的数组，并初始化这些结构的名字部分。用函数执行d、e、f和g中描述的任务。
d. 以交互的方式获取每个学生的成绩，提示用户输入学生的姓名和分数。把分数储存到grade数组相应的结构中。可以在main()函数或其他函数中用循环来完成。
e. 计算每个结构的平均分，并把计算后的值赋给合适的成员。
f. 打印每个结构的信息。
g. 打印班级的平均分，即所有结构的数值成员的平均值。
``` c
#include <stdio.h>
struct tl_name
{
    char name[10];
    char surname[10];
};
struct tl_student
{
    struct tl_name fullname;
    double grade[3];
    double ave;
};
char *s_gets(char *st, int n);
void d_fun(struct tl_student *);
double get_score_parameter(double *); // 靠指针修改数值
double get_score_Returnvalue();       // 返回指定数值       合并这个函数很简单 但代码会变难看 所以另开了一个函数
void e_fun(struct tl_student *);
void f_fun(const struct tl_student *); // 我觉得大部分情况下还是指针好一点
void g_fun(const struct tl_student *); // 如果想要结构副本 就还是传递结构地址 然后函数指针参数赋值同类型结构来得到副本
#define CSIZE 4
int main(void)
{
    struct tl_student student[CSIZE] =
        {// 和初始化数组没太大差别 方法太多
         {.fullname.name = "bei", "liu"},
         {.fullname.name = "fei", "zhang"},
         {.fullname.name = "yu", "guan"},
         {.fullname.name = "yi", "hou"}};
    d_fun(student);
    e_fun(student);
    f_fun(student);
    g_fun(student);
    return 0;
}
void g_fun(const struct tl_student *student)
{
    double total = 0;
    for (int i = 0; i < CSIZE; i++) // 所有同学的总成绩
    {
        for (int j = 0; j < 3; j++) // 一位同学的总成绩
            total += student[i].grade[j];
    }
    printf("所有同学的平均成绩为%.lf\n", total / CSIZE);
}
void f_fun(const struct tl_student *student)
{
    for (int i = 0; i < CSIZE; i++)
    {
        printf("%10s %10s同学的语文成绩为 %3.lf, 数学成绩为 %3.lf, 英语成绩为 %3.lf, 三科平均分为%3.lf\n", student[i].fullname.surname, student[i].fullname.name, student[i].grade[0], student[i].grade[1], student[i].grade[2], student[i].ave);
    }
}
void e_fun(struct tl_student *student)
{
    double total;
    for (int i = 0; i < CSIZE; i++)
    {
        total = 0;
        for (int j = 0; j < 3; j++) // 一位同学的平均成绩
            total += student[i].grade[j];
        student[i].ave = total / 3;
    }
}
void d_fun(struct tl_student *student) // 首先解决指定学生的问题 像1的遍历对比检测
{                                      // 要求用户输入全称  然后and 也就是 姓和名都要对比检测 && 通过
    char student_surname[10];          // 在用户输入姓后 提示所有有这个姓的人 就四个元素还是不写了吧 没啥技术含量
    char student_name[10];
    char *subject[3] = {"语文", "数学", "英语"};
    int no_stuname = 1; // 0 代表没有这个同学 1代表有这个同学
    int i, j;
    puts("请输入学生的姓");
    while (s_gets(student_surname, 10) != NULL && student_surname[0] != '\0')
    {
        no_stuname = 1;
        puts("请输入学生的名");
        s_gets(student_name, 10);
        for (i = 0; i < CSIZE; i++) // 我的编译器是支持我指针转数组的   然后注意 如果要用指针递增的话别忘了for循环外初始化(还原)指针指向的地址
        {                           // 这就需要一个同类型的指针来保存这个地址了 比指针多了一个步骤吧
            if ((strcmp(student_surname, student[i].fullname.surname) == 0) && (strcmp(student_name, student[i].fullname.name) == 0))
                break;
            if (i == (CSIZE - 1))
            {
                printf("没有找到%s %s同学的信息\n", student_surname, student_name);
                no_stuname = 0;
            }
        }
        if (no_stuname == 0) // 这里嵌套了而continue均只跳过内循环 所有用了这个法子
        {
            puts("请输入下一位学生的姓 (空行退出)");
            continue;
        }
        for (j = 0; j < 3; j++)
        {
            printf("请输入%s %s同学的%s成绩", student[i].fullname.surname, student[i].fullname.name, subject[j]);
            get_score_parameter(&student[i].grade[j]);
        }
        while (getchar() != '\n')
            continue; /* 清理输入行*/
        puts("请输入下一位学生的姓 (空行退出)");
    }
}
double get_score_parameter(double *pt)
{
    while (scanf("%lf", pt) != 1 || *pt < 0 || *pt > 100)
    {
        while (getchar() != '\n')
            ;
        puts("输入错误");
    }
}
double get_score_Returnvalue()
{
    double score;
    while (scanf("%lf", &score) != 1 || score < 0 || score > 100)
    {
        while (getchar() != '\n')
            ;
        puts("输入错误");
    }
    return score;
}
char *s_gets(char *st, int n)
{
    char *ret_val;
    char *find;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        find = strchr(st, '\n'); // 查找换行符
        if (find)                // 如果地址不是NULL，
            *find = '\0';        // 在此处放置一个空字符
        else
            while (getchar() != '\n')
                continue; // 清理输入行中剩余的字符
    }
    return ret_val;
}
```
----------

### 第六题
6. 一个文本文件中保存着一个垒球队的信息。每行数据都是这样排列：
4 Jessie Joybat 5 2 1 1
第1项是球员号，为方便起见，其范围是0～18。第2项是球员的名。第3项是球员的姓。名和姓都是一个单词。第4项是官方统计的球员上场次数。 接着3项分别是击中数、走垒数和打点（RBI）。文件可能包含多场比赛的 数据，所以同一位球员可能有多行数据，而且同一位球员的多行数据之间可能有其他球员的数据。编写一个程序，把数据储存到一个结构数组中。该结构中的成员要分别表示球员的名、姓、上场次数、击中数、走垒数、打点和 安打率（稍后计算）。可以使用球员号作为数组的索引。该程序要读到文件结尾，并统计每位球员的各项累计总和。
世界棒球统计与之相关。例如，一次走垒和触垒中的失误不计入上场次数，但是可能产生一个RBI。但是该程序要做的是像下面描述的一样读取和处理数据文件，不会关心数据的实际含义。
要实现这些功能，最简单的方法是把结构的内容都初始化为零，把文件中的数据读入临时变量中，然后将其加入相应的结构中。程序读完文件后，应计算每位球员的安打率，并把计算结果储存到结构的相应成员中。计算安打率是用球员的累计击中数除以上场累计次数。这是一个浮点数计算。最后，程序结合整个球队的统计数据，一行显示一位球员的累计数据。
``` c   // test.txt文件
8 John Wick 1 9 9 9
8 John Wick 5 1 8 4
1 David Tennant 2 0 1 7
2 Hugo Weaving 3 0 4 4
3 Matt Smith 4 7 4 2
4 Jessie Joybat 5 2 1 1
5 Karen Sheila 6 9 8 7
4 Jessie Joybat 7 5 1 6
7 Granville Jones 5 2 3 1
8 John Wick 1 6 3 7
9 Chuck Langer 7 5 9 3
11 Alan White 6 7 8 0
11 Alan White 6 1 8 7
13 Tilda Swinton 1 3 8 0
2 Hugo Weaving 3 8 7 5
8 John Wick 5 1 8 4
16 Alan White 2 8 5 7
4 Jessie Joybat 3 1 9 8
2 Hugo Weaving 2 9 7 8
```
 ``` c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define FILE_ "test.txt"
#define P_num 18 // 声明《CPP》在这题之前并没有教relloc 其次，第二段文字中倒数第二句 球员号可以直接作为数组的索引
struct TL_team   // 同时这段第一句 其范围是0~18 ，作者做了限制 意以表明这个程序就18了 所以你会发现我的程序非常简单
{                // 使用球员号当作数组索引就少了非常多的代码
    int num; // 球员号
    struct
    {
        char surname[10];
        char name[10];
    };
    int G;      // G - Games Played 上场次数
    int AB;     // AB - At Bats - 击中数
    int SB;     // steala base 走垒数
    int RBI;    // AB/RBI - At-Bats per Runs Batted In - 打点
    double AVG; // AVG - Batting Average 安打率
};
int main(void)
{
    struct TL_team team[P_num] = {0}, temp;
    FILE *fp;
    if ((fp = fopen(FILE_, "r")) == NULL)
    {
        fprintf(stdout, "Can't open \"%s\" file.\n", FILE_); // fs接收数值失败
        exit(EXIT_FAILURE);
    }
    while (fscanf(fp, "%d %s %s %d %d %d %d\n", &temp.num, temp.surname, temp.name, &temp.G, &temp.AB, &temp.SB, &temp.RBI) == 7)
    {
        strcpy(team[temp.num].surname, temp.surname);
        strcpy(team[temp.num].name, temp.name);
        team[temp.num].num = temp.num;
        team[temp.num].G += temp.G;
        team[temp.num].AB += temp.AB;
        team[temp.num].SB += temp.SB;
        team[temp.num].RBI += temp.RBI;
    }
    for (int i = 1; i < P_num; i++) // 没有球员的球员号为0
    {
        if (team[i].num != 0) // 根据球员号输出
        {
            team[i].AVG = (double)team[i].AB / (double)team[i].G;
            printf("%2d号球员%10s %10s上场%2d次,击中%2d次,走垒%2d次,打点%2d次, 安打率为%.2lf\n", team[i].num, team[i].surname, team[i].name, team[i].G, team[i].AB, team[i].SB, team[i].RBI, team[i].AVG);
        }
    }
    return 0;
}
```
----------

### 第七题
7. 修改程序清单 14.14，从文件中读取每条记录并显示出来，允许用户删除记录或修改记录的内容。如果删除记录，把空出来的空间留给下一个要读入的记录。要修改现有的文件内容，必须用"r+b"模式，而不是"a+b"模式。而且，必须更加注意定位文件指针，防止新加入的记录覆盖现有记录。最简单的方法是改动储存在内存中的所有数据，然后再把最后的信息写入文件。跟踪的一个方法是在book结构中添加一个成员表示是否该项被删除。
``` c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAXTITL 40
#define MAXAUTL 40
#define MAXBKS 10 /* 最大书籍数量 */
char *s_gets(char *st, int n);
struct book
{
    char title[MAXTITL];
    char author[MAXAUTL];
    float value;
};
void add_book(struct book *, int);
void mod_book(struct book *);
void del_book(struct book *);
int main(void)
{
    struct book library[MAXBKS] = {0}; /* 结构数组 */
    int count = 0, index, filecount, status = 0;
    FILE *pbooks;
    int size = sizeof(struct book);
    if ((pbooks = fopen("book.dat", "r+b")) == NULL) // r+模式要求文件必须存在
    {
        if ((pbooks = fopen("book.dat", "w+b")) == NULL) // 所以用户第一次使用程序时将执行这个语句
        {
            fputs("Can't open book.dat file\n", stderr);
            status = 1; // 说明book.dat是新建的 所以就没必要进行下面的接收结构数组并打印了
            exit(1);
        }
    }
    rewind(pbooks); /* 定位到文件开始 */
    if (status == 0)
    {
        while (count < MAXBKS && fread(&library[count], size, 1, pbooks) == 1)
        {
            if (count == 0)
                puts("Current contents of book.dat:");
            if (library[count].title[0] != '\0')
                printf("%s by %s: $%.2f\n", library[count].title, library[count].author, library[count].value);
            count++;
        }
    }
    else
        puts("请输入下面菜单中的选项");
    filecount = count;               /// 这个语句
    for (int i = 0; i < MAXBKS; i++) // 检测图书馆还能不能放书
    {
        if (library[i].title[0] == '\0') // 因规定任何数据不能为空 所以这一条应该就不会有什么问题了
            break;
        else if (library[MAXBKS - 1].title[0] != '\0') // 最后一本也不为空
        {
            fputs("The book.dat file is full.", stderr);
            exit(2);
        }
    }
    puts("a.添加书籍    b.修改书籍    c.删除书籍    d.退出");
    int ch;
    while ((ch = getchar()) != 'd')
    {
        fflush(stdin);
        switch (ch)
        {
        case 'a':
            add_book(library, count);
            break;
        case 'b':
            mod_book(library);
            break;
        case 'c':
            del_book(library);
            break;
        default:
            puts("输入错误, 请输入下面菜单中的选项");
            puts("a.添加书籍    b.修改书籍    c.删除书籍    d.退出");
            continue;
            break;
        }
        for (int i = 0; i < MAXBKS; i++) // 打印在执行函数后的结构数组状态
        {
            if (library[i].title[0] != '\0') // 因规定任何数据不能为空 所以这一条应该就不会有什么问题了
                printf("%d号 《%s》 by %s: $%.2f\n", i, library[i].title, library[i].author, library[i].value);
        }
        puts("a.添加书籍    b.修改书籍    c.删除书籍    d.退出");
    }
    puts("以下数据将会保存在文件:");
    for (int i = 0; i < MAXBKS; i++)
    {
        if (library[i].title[0] != '\0') // 因规定任何数据不能为空 所以这一条应该就不会有什么问题了
            printf("%d号 《%s》 by %s: $%.2f\n", i, library[i].title, library[i].author, library[i].value);
    }
    rewind(pbooks);
    fwrite(&library[0], size, MAXBKS, pbooks);
    puts("Bye.\n");
    fclose(pbooks);
    return 0;
}
void mod_book(struct book *library)
{
    int i;
    for (i = 0; i < MAXBKS; i++)
    {
        if (library[i].title[0] != '\0') // 因规定任何数据不能为空 所以这一条应该就不会有什么问题了
            printf("%d号 《%s》 by %s: $%.2f\n", i, library[i].title, library[i].author, library[i].value);
    }
    struct book temp;
    puts("请问你要修改几号书籍");
    int index;
    while ((scanf("%d", &index) != 1) || (index > 10) || (index < 0)) // 书籍保护 防止垃圾值
    {
        puts("输入错误 请选择以下图书");
        for (i = 0; i < MAXBKS; i++)
        {
            if (library[i].title[0] != '\0') // 因规定任何数据不能为空 所以这一条应该就不会有什么问题了
                printf("%d号 《%s》 by %s: $%.2f\n", i, library[i].title, library[i].author, library[i].value);
        }
        continue;
    }
    fflush(stdin);
    puts("Please modify new book titles.");
    puts("Press [enter] at the start of a line to stop.");
    while (s_gets(temp.title, MAXTITL) != NULL && temp.title[0] != '\0')
    {
        puts("Now enter the author.");
        s_gets(temp.author, MAXAUTL);
        puts("Now enter the value.");
        scanf("%f", &temp.value);
        library[index] = temp; // 赋值
        while (getchar() != '\n')
            continue; /* 清理输入行 */
        break;
    }
}
void add_book(struct book *library, int count) // count为当前数组中有多少个结构
{
    struct book temp;
    int i = 0;
    puts("Please add new book titles.");
    puts("Press [enter] at the start of a line to stop.");
    for (i = 0; i < MAXBKS; i++)
    {
        if (library[i].title[0] == '\0') // 如果书名是空的 因为规定数据不能为空 所以这一条应该就不会有什么问题了
            break;
    }
    while (s_gets(temp.title, MAXTITL) != NULL && temp.title[0] != '\0')
    {
        puts("Now enter the author.");
        s_gets(temp.author, MAXAUTL);
        puts("Now enter the value.");
        scanf("%f", &temp.value);
        library[i] = temp; // 赋值
        while (getchar() != '\n')
            continue; /* 清理输入行 */
        for (; i < MAXBKS; i++)
        {
            if (library[i].title[0] == '\0') // 如果书名是空的 因为规定数据不能为空 所以这一条应该就不会有什么问题了
                break;
        }
        puts("Enter the next title.");
        puts("Press [enter] at the start of a line to stop.");
    }
}
void del_book(struct book *library)
{
    struct book empty = {"", "", 0};
    for (int i = 0; i < MAXBKS; i++)
    {
        if (library[i].title[0] != '\0') // 因规定任何数据不能为空 所以这一条应该就不会有什么问题了
            printf("%d号 《%s》 by %s: $%.2f\n", i, library[i].title, library[i].author, library[i].value);
    }
    puts("请问你要删除几号书籍");
    int index;
    scanf("%d", &index);
    fflush(stdin);
    library[index] = empty;
    puts("删除完成");
}
char *s_gets(char *st, int n)
{
    char *ret_val;
    char *find;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        find = strchr(st, '\n'); // 查找换行符
        if (find)                // 如果地址不是NULL，
            *find = '\0';        // 在此处放置一个空字符
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```
----------

### 第八题
8. 巨人航空公司的机群由12个座位的飞机组成。它每天飞行一个航班。根据下面的要求，编写一个座位预订程序。
a.该程序使用一个内含 12 个结构的数组。每个结构中包括：一个成员表示座位编号、一个成员表示座位是否已被预订、一个成员表示预订人的名、一个成员表示预订人的姓。
b.该程序显示下面的菜单：
To choose a function, enter its letter label:
a) Show number of empty seats
b) Show list of empty seats
c) Show alphabetical list of seats
d) Assign a customer to a seat assignment
e) Delete a seat assignment
f) Quit
c.该程序能成功执行上面给出的菜单。选择d)和e)要提示用户进行额外输入，每个选项都能让用户中止输入。
d.执行特定程序后，该程序再次显示菜单，除非用户选择f)。
``` c
/*
9. 巨人航空公司（编程练习 8）需要另一架飞机（容量相同），每天飞4 班（航班 102、311、444 和519）。把程序扩展为可以处理4个航班。用一个顶层菜单提供航班选择和退出。选择一个特定航班，就会出现和编程练习 8类似的菜单。但是该菜单要添加一个新选项：确认座位分配。而且，菜单中的退出是返回顶层菜单。每次显示都要指明当前正在处理的航班号。另外，座位分配显示要指明确认状态。
*/
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct airplane
{
    int i;
    int status;
    struct
    {
        char surname[10];
        char name[10];
    };
};
static char menu[200] = {"要选择函数，请输入其字母标签：\na） 显示空座位数      b） 显示空座位列表\nc） 显示按字母顺序排列的座位列表\nd） 为客户分配座位    e） 删除座位分配\nf） 退出"};
#define NUM 12
void EOES(struct airplane *); // 空座位数量
void LOES(struct airplane *); // 空座位列表
void ALOS(struct airplane *); // 按字母顺序排列的座位列表
void ACTS(struct airplane *); // 为客户分配座位
void DASA(struct airplane *); // 删除座位分配
char *s_gets(char *st, int n);
int main(void)
{
    struct airplane seats[NUM] = {0};
    for (int i = 0; i < NUM; i++) // 座位号初始化 如果不这样 那ALOS函数会出现一些小问题
        seats[i].i = (i + 1);
    puts(menu);
    int ch;
    while ((ch = getchar()) != 'f')
    {
        fflush(stdin);
        switch (ch)
        {
        case 'a':
            system("CLS");
            EOES(seats);
            break;
        case 'b':
            system("CLS");
            LOES(seats);
            break;
        case 'c':
            system("CLS");
            ALOS(seats);
            break;
        case 'd':
            system("CLS");
            ACTS(seats);
            break;
        case 'e':
            system("CLS");
            DASA(seats);
            break;
        default:
            system("CLS");
            puts("输入错误, 请输入下面菜单中的选项");
            puts(menu);
            continue;
        }
        puts(menu);
    }
    return 0;
}
void EOES(struct airplane *seats)
{
    int num = 0;
    for (int i = 0; i < NUM; i++)
    {
        if (seats[i].status == 0)
            num++;
    }
    printf("目前飞机上还有%d个空位\n", num);
}
void LOES(struct airplane *seats)
{
    for (int i = 0; i < NUM; i++)
    {
        if (seats[i].status == 0)
            printf("%2d号座位 未预定\n", i + 1);
    }
}
void ALOS(struct airplane seats[]) // 因为实现方法原因这里给个副本
{
    struct airplane temp;
    for (int i = 0; i < NUM; i++)
    {
        for (int j = i; j < NUM; j++)
        {
            if (strcmp(seats[i].surname, seats[j].surname) > 0)
            {
                temp = seats[i];
                seats[i] = seats[j];
                seats[j] = temp;
            }
        }
    }
    for (int i = 0; i < NUM; i++)
    {
        if (seats[i].status)
            printf("%2d号 已预定 %s %s\n", seats[i].i, seats[i].surname, seats[i].name);
        else
            printf("%2d号 未预定\n", seats[i].i);
    }
}
void ACTS(struct airplane *seats)
{
    int index;
    puts("请问你要选择几号座位 (q.退出)");
    while (scanf("%d", &index) == 1)
    {
        fflush(stdin);
        if (seats[index - 1].status)
            printf("%d号座位已经有人预定了", index);
        else
        {
            seats[index - 1].status = 1;
            seats[index - 1].i = index; // warn
            puts("请输入你的姓氏");
            s_gets(seats[index - 1].surname, 10);
            puts("请输入你的名字");
            s_gets(seats[index - 1].name, 10);
            puts("预定成功");
            break;
        }
    }
    fflush(stdin);
}
void DASA(struct airplane *seats)
{
    struct airplane temp = {0};
    for (int i = 0; i < NUM; i++)
    {
        if (seats[i].status)
            printf("%2d号 已预定 %s %s\n", i + 1, seats[i].surname, seats[i].name);
    }
    puts("请问要删除哪个预定过的座位 (q.退出)");
    int index;
    while (scanf("%d", &index) == 1)
    {
        if (seats[index - 1].status == 0)
        {
            puts("这个座位并没有被预定");
            continue;
        }
        fflush(stdin);
        seats[index - 1] = temp;
        puts("删除成功");
        break;
    }
}
char *s_gets(char *st, int n)
{
    char *ret_val;
    char *find;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        find = strchr(st, '\n'); // 查找换行符
        if (find)                // 如果地址不是NULL，
            *find = '\0';        // 在此处放置一个空字符
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```
----------

### 第九题
9. 巨人航空公司（编程练习 8）需要另一架飞机（容量相同），每天飞4 班（航班 102、311、444 和519）。把程序扩展为可以处理4个航班。用一个顶层菜单提供航班选择和退出。选择一个特定航班，就会出现和编程练习 8类似的菜单。但是该菜单要添加一个新选项：确认座位分配。而且，菜单中的退出是返回顶层菜单。每次显示都要指明当前正在处理的航班号。另外，座位分配显示要指明确认状态。
``` c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct airplane
{
    int i;
    int status;
    struct
    {
        char surname[10];
        char name[10];
    };
};
static char menu[200] = {"要选择函数，请输入其字母标签：\na） 显示空座位数      b） 显示空座位列表\nc） 显示按字母顺序排列的座位列表\nd） 为客户分配座位    e） 删除座位分配\nf） 退出"};
static char flight_sec[100] = {"请选择一架航班 (q.退出)\n1.歼200 102    2.B-29   311\n3.EP-33 444    4.CF-100 519"};
void MAME(int);
void EOES(struct airplane *); // 空座位数量
void LOES(struct airplane *); // 空座位列表
void ALOS(struct airplane *); // 按字母顺序排列的座位列表
void ACTS(struct airplane *); // 为客户分配座位
void DASA(struct airplane *); // 删除座位分配
char *s_gets(char *st, int n);
int main(void)
{
    puts(flight_sec);
    int T, F;
    while ((T = getchar()) != 'q')
    {
        fflush(stdin);
        switch (T)
        {
        case '1':
            MAME(1);
            break;
        case '2':
            MAME(2);
            break;
        case '3':
            MAME(3);
            break;
        case '4':
            MAME(4);
            break;
        default:
            system("CLS");
            puts("输入错误 请输入以下航班序号");
            puts(flight_sec);
            continue;
        }
        system("CLS");
        puts(flight_sec);
    }
    return 0;
}
void MAME(int F)
{
    struct airplane seats[4][12] = {0}; // 先来做一些二维数组的改变
    for (int i = 0; i < 4; i++)
    {
        for (int j = 0; j < 12; j++)
            seats[i][j].i = (j + 1);
    }
    char *Fname[4] = {
        "歼200 102",
        "B-29 311",
        "EP-33 444",
        "CF-100 519"};
    system("CLS");
    printf("当前航班为%d号%s航班\n", F, Fname[F - 1]);
    puts(menu);
    int ch;
    while ((ch = getchar()) != 'f') // 这边做成一个函数 然后就是一维那边是作为一个参数  传过来的
    {
        fflush(stdin);
        switch (ch)
        {
        case 'a':
            system("CLS");
            printf("当前航班为%d号%s航班\n", F, Fname[F - 1]);
            EOES(seats[F - 1]);
            break;
        case 'b':
            system("CLS");
            printf("当前航班为%d号%s航班\n", F, Fname[F - 1]);
            LOES(seats[F - 1]);
            break;
        case 'c':
            system("CLS");
            printf("当前航班为%d号%s航班\n", F, Fname[F - 1]);
            ALOS(seats[F - 1]);
            break;
        case 'd':
            system("CLS");
            printf("当前航班为%d号%s航班\n", F, Fname[F - 1]);
            ACTS(seats[F - 1]);
            break;
        case 'e':
            system("CLS");
            printf("当前航班为%d号%s航班\n", F, Fname[F - 1]);
            DASA(seats[F - 1]);
            break;
        default:
            system("CLS");
            puts("输入错误, 请输入下面菜单中的选项");
            puts(menu);
            continue;
        }
        puts(menu);
    }
    fflush(stdin);
}
void EOES(struct airplane *seats)
{
    int num = 0;
    for (int i = 0; i < 12; i++)
    {
        if (seats[i].status == 0)
            num++;
    }
    printf("目前飞机上还有%d个空位\n", num);
}
void LOES(struct airplane *seats)
{
    for (int i = 0; i < 12; i++)
    {
        if (seats[i].status == 0)
            printf("%2d号座位 未预定\n", i + 1);
    }
}
void ALOS(struct airplane seats[]) // 因为实现方法原因这里给个副本
{
    struct airplane temp;
    for (int i = 0; i < 12; i++)
    {
        for (int j = i; j < 12; j++)
        {
            if (strcmp(seats[i].surname, seats[j].surname) > 0)
            {
                temp = seats[i];
                seats[i] = seats[j];
                seats[j] = temp;
            }
        }
    }
    for (int i = 0; i < 12; i++)
    {
        if (seats[i].status)
            printf("%2d号 已预定 %s %s\n", seats[i].i, seats[i].surname, seats[i].name);
        else
            printf("%2d号 未预定\n", seats[i].i);
    }
}
void ACTS(struct airplane *seats)
{
    int index;
    struct airplane temp;
    puts("请问你要选择几号座位 (q.退出)");
    while (scanf("%d", &index) == 1)
    {
        fflush(stdin);
        if (seats[index - 1].status)
        {
            printf("%d号座位已经有人预定了\n", index);
            puts("请问你要选择几号座位 (q.退出)");
        }
        else
        {
            temp.status = 1;
            temp.i = index;
            puts("请输入你的姓氏");
            s_gets(temp.surname, 10);
            puts("请输入你的名字");
            s_gets(temp.name, 10);
            printf("%2d号 %s %s\n确认要预定吗(Y ? N)", temp.i, temp.surname, temp.name);
            char st;
            if ((st = getchar()) == 'Y')
            {
                seats[index - 1] = temp;
                system("CLS");
                puts("预定成功");
            }
            break;
        }
    }
    fflush(stdin);
}
void DASA(struct airplane *seats)
{
    struct airplane temp = {0};
    for (int i = 0; i < 12; i++)
    {
        if (seats[i].status)
            printf("%2d号 已预定 %s %s\n", i + 1, seats[i].surname, seats[i].name);
    }
    puts("请问要删除哪个预定过的座位 (q.退出)");
    int index;
    while (scanf("%d", &index) == 1)
    {
        if (seats[index - 1].status == 0)
        {
            puts("这个座位并没有被预定");
            continue;
        }
        fflush(stdin);
        seats[index - 1] = temp;
        puts("删除成功");
        break;
    }
}
char *s_gets(char *st, int n)
{
    char *ret_val;
    char *find;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        find = strchr(st, '\n'); // 查找换行符
        if (find)                // 如果地址不是NULL，
            *find = '\0';        // 在此处放置一个空字符
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```
----------

### 第十题
10. 编写一个程序，通过一个函数指针数组实现菜单。例如，选择菜单中的 a，将激活由该数组第 1个元素指向的函数。
``` c
#include <stdio.h>
int fun_a(char *);
double fun_b(char *);
char fun_c(char *);
typedef void (*pfun)(char *);   // 好像是不能指向任意类型的参数的
int main(void)
{
    pfun fun[3] = {
        fun_a,
        fun_b,
        fun_c};
    puts("a.fun_a    b.fun_b    c.fun_c");
    int ch;
    ch = getchar();
    switch (ch)
    {
    case 'a':
        fun[0]("hello");
        break;
    case 'b':
        fun[1]("a");
        break;
    case 'c':
        fun[2]("3.14");
        break;
    default:
        break;
    }
    return 0;
}
int fun_a(char *str)
{
    printf("%s\n", str);
    return 0;
}
double fun_b(char *i)
{
    printf("%c\n", *i);
    return 3.14;
}
char fun_c(char *pt)
{
    printf("Π = %s\n", pt);
    return 'a';
}
```
----------

### 第十一题
11. 编写一个名为transform()的函数，接受4个参数：内含double类型数据的源数组名、内含double类型数据的目标数组名、一个表示数组元素个数的int类型参数、函数名（或等价的函数指针）。transform()函数应把指定函数应用于源数组中的每个元素，并把返回值储存在目标数组中。例如：
transform(source, target, 100, sin);
该声明会把target[0]设置为sin(source[0])，等等，共有100个元素。在一个程序中调用transform()4次，以测试该函数。分别使用math.h函数库中的两个函数以及自定义的两个函数作为参数。
``` c
#include <stdio.h>
#include <math.h>
#include <stdlib.h>
#define S 100
void transfrom(double *, double *, int, double (*pfun)(double));
double fun_a(double);
double fun_b(double);
int main(void)
{
    double target[100], source[100] = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    transfrom(source, target, S, sqrt);
    transfrom(source, target, S, cbrt);
    transfrom(source, target, S, fun_a);
    transfrom(source, target, S, fun_b);
    return 0;
}
void transfrom(double *source, double *target, int i, double (*pfun)(double))
{
    for (int j = 0; j < 10; j++) // 为了方便显示 改成了10
    {
        target[j] = pfun(source[j]);
        printf("%.1lf ", target[j]);
    }
    putchar('\n');
}
double fun_a(double num)
{
    srand((int)num);
    return rand();
}
double fun_b(double num)
{
    return num / num;
}
```