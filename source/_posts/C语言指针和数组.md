---

title: C语言中指针和数组关系统计
date: 2020-01-02 23:08:00
tags: [教程]
categories: C语言

---



由于指针和数组的关系过于繁杂 所以写一篇统计对比来巩固且用于日后参考
## 指针和数组
``` c
    int va  =  10;        //声明一个int型变量va，且初始化其值为10；
    int *pt = &va;        //声明一个int型指针pt，指向变量va的地址
    printf("%d",  va);    //变量va的数值 10
    printf("%d", *pt);    //解引用指针pt后的数值 10

    printf("%p",  pt);    //指针pt的数值        例：61fe1c
    printf("%p", &va);    //变量va的物理地址    例：61fe1c

    printf("%x", &pt);    //十六进制指针pt的物理地址    例：61fe10
```


## 数组基本
``` c
    int array[7] = {0, 1, 2, 3, 4, 5, 6};   //声明一个int型数组array，项数为7，初始化元素为
    int array[7] = {0, 1, [3] = 2, [4] = 3, 4, 5, 6};   //C99增加的一个特性 用于初始化指定的数组元素    当然如果操作不当会出现一些小问题 这里就不解释了
    int array[4][4] =
    {
        {0, 1, 2, 3},
        {1, 1, 2, 3},
        {2, 1, 2, 3},
        {3, 1, 2, 3}
    };                              //二维数组声明

    for (int i = 0; i < 7; i++)     //打印一维数组的一种方法
        printf("%d\n", array[i]);
    //打印二维数组则需要嵌套一个for
    for (int i = 0; i < 4; i++)
        for (int j = 0; j < 4; j++)
            printf("%d\n", array[i][j]);


```

<!--more-->

## 指针和多维数组
```c
    int array[4][4] =
        {{1, 2, 3, 4},
         {5, 6, 7, 8},
         {9, 10, 11, 12},
         {13, 14, 15, 16}};

    //array是这个数组首元素的地址
    //所以array = &array[0]
    //而array[0]又是array[0][0]的首元素的地址
    //所以array[0] = &array[0][0]

    //因为
    //array[1] == *(array + 1)      //相同数值
    //&array[1] == array + 1        //相同地址      也就是指针形式
    //所以可有以下代码行

    //指针形式
    printf("%d\n", array);                        //二维数组首元素的地址
    printf("%d\n", array + 1);                    //二维数组第二个元素的地址
    printf("%d\n", *(array + 1));                 //二维数组第二个元素首元素的地址
    printf("%d\n", *(array + 1) + 1);             //二维数组第二个元素的第二个元素的地址
    printf("%d\n", *(*(array + 1) + 1));          //二维数组第二个元素的第二个元素的数值
    //数组形式
    printf("%d\n", &array[0]);                    //二维数组首元素的地址
    printf("%d\n", &array[1]);                    //二维数组第二个元素的地址
    printf("%d\n", &array[1][0]);                 //二维数组第二个元素首元素的地址
    printf("%d\n", &array[1][1]);                 //二维数组第二个元素的第二个元素的地址
    printf("%d\n", array[1][1]);                  //二维数组第二个元素的第二个元素的数值
    //半指针半数组形式  就举俩例子吧  说明有这个写法 用多了估计会走火入魔
    printf("%d\n", &*(array[1] + 1));             //二维数组第二个元素的第二个元素的地址
    printf("%d\n", *(array[1] + 1));              //二维数组第二个元素的第二个元素的数值

    //第十章的编程练习答案里我把三种形式各用了一遍 可以看一下都有些什么样的优势(当然包括半指针和半数组形式)
```


## 指针数组
``` C
    int *pt[4];
    //pt是一个内含四个指针元素的数组，每个元素都指向int的指针
    //用于指向四个数值 使用以下示例
    char * pt[4] = {
        "Hello,World!",
        "Three,Body!",
        "I'm,Hunger",
        "Candy,Cola"};
        for(int i = 0; i < 4; i++)
            printf("%s\n", pt[i]);
```


## 数组指针(指向多维数组的指针)·
``` C
    int (* pt)[4];
//pt指向一个内含四个int类型数值的数组
    int array[4][4] =
        {{1, 2, 3, 4},
         {5, 6, 7, 8},
         {9, 10, 11, 12},
         {13, 14, 15, 16}};
    pt = &array;
    printf("%d", pt[0][0]); //然后就可以使用指针和多维数组里的那些操作了

```


## 指向指针的指针
```c
    int a =100;
    int *p1 = &a;
    int **p2 = &p1;
    printf("%d\n", a);
    printf("%d\n", *p1);
    printf("%d\n", **p2);
    //为什么需要加两个解引用符号是因为
    int *pt = &p1;
    printf("%d\n", *pt);    //这样给的是个地址 且不能再次解引用
```


## void指针、NULL指针和NUL
```c
    void指针    //由于void没有特性的类型，因此它可以指向任何类型的数据
    因为现在我用不到 所以就先不记了

    NULL指针在stdio.h中被定义为    #define NULL ((void *)0)
    (void *)0 把数值0显式转换为void * 类型

    NUL是ASCII中的第一个字符的名称　被定义为'/0'
    而数字0对应十进制48  所以不要把NUL和NULL搞混　也不要把'/0'和0搞混
```

## 函数、数组和指针
```c
    #define ROWS
    #define COLS 4
    //声明数组形参原型  两种类型等效 但只有指针形式可以使用递增
    //一维数组操作函数
    void put1(int  *pt, int n);  //指针形式
    void put2(int  *  , int  );  //指针形式 省略形参
    void put3(int pt[], int n);  //数组形式
    void put4(int   [], int  );  //数组形式 省略形参    //把要操作的数组名地址作为第一个参数，然后是这个数组的长度


    //二维数组操作函数
    void put5(int (*pt)[COLS], int rows);       //半指针半数组形式
    void put6(int (*  )[COLS], int     );       //半指针半数组形式 省略形参
    void put7(int  pt[][COLS], int rows);       //数组形式
    void put8(int    [][COLS], int     );       //数组形式 省略形参     //把要操作的数组名作为第一个参数，然后是这个数组维度数

    //带变长数组形参的二维数组操作函数
    void puta(int rows, int cols, int ar[rows][cols]);   //数组形式
    void putb(int     , int cols, int   [    ][cols]);   //数组形式 省略形参    //多维数组的声明必须具有除第一个维度以外的所有维度的边界
```


## 指针函数和函数指针
``` c
指针函数
    像strcpy()函数，strcat()函数，strcmp()函数，这些都是指针函数用来返回一个指针 注意：不要返回局部变量

函数指针

```


## 指针操作 295


## 参数中带函数的函数
```
def add(x, y, f):           //abs是一个求绝对值的函数
    return f(x) + f(y)
print(add(-5, 6, abs))
```