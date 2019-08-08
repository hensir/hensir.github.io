---

title: 如何用MinGW-x64在VSCode编译和调试C/C++
date: 2019-08-07 13:00:00
tags: [VSCode,教程]
categories: 教程

---



# 前言
我的环境如下：
平台：Windows10 x64
[Mingw-w64](http://mingw-w64.org/doku.php)版本：x86_64-8.1.0-posix-seh-rt_v6-rev0
[VSCode](https://code.visualstudio.com/)版本：1.36.1 x64
由于Mingw-w64在线安装需要梯子，所以这里推荐大家安装由SOURCEFORGE托管的Mingw-w64绿色安装包
下载地址为：https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/
![下载示图](https://s2.ax1x.com/2019/08/07/eIUlVI.png)

----------

<!--more-->

# Mingw-w64

## 安装Mingw-w64
在SOURCEFORGE里下载完压缩包之后直接把里面的内容解压出来就能用了
![解压示图](https://s2.ax1x.com/2019/08/07/eIdsvF.png)
这里我解压到了C盘的根目录下 你们随意

----------

## 配置环境变量

![配置示图](https://s2.ax1x.com/2019/08/07/eIgKs0.png)
右击计算机-属性-高级系统设置-环境变量-Path（系统变量）-新建-输入你的mingw64下的bin文件夹地址

----------

## 检测环境变量是否搭建成功
![检测示图](https://s2.ax1x.com/2019/08/07/eIWqld.png)


----------


# VSCode

## 安装VScode

----------

## 安装C/C++扩展
![安装扩展示图](https://s2.ax1x.com/2019/08/07/eIoUlF.png)
也可以安装下中文包 搜索chinese第一个就是

----------

## 创建工作区

### 新建一个文件夹来作为你的C项目地址（名称中最好不要有空格和中文）

----------

### 用VSCode打开这个文件夹

----------

### 如图新建一个名为.vscode的文件夹就行了![创建示图](https://s2.ax1x.com/2019/08/07/eI7xJ0.png) 

----------

### 在.vscode文件夹里创建一个名为[launch.json](https://github.com/microsoft/vscode-cpptools/blob/master/launch.md)的文件
 然后输入以下代码(以下配置皆为VSCode默认生成的模板)
 ```
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "gdb(lunch)",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "C:/mingw64/bin/gdb.exe", //这行地址改为gdb的地址
            "setupCommands": [                          //如果你把mingw64解压到了D盘的根目录下
                {                                       //那这里就写D:/mingw64/bin/gdb.exe
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "gcc build"
        }
    ]
}

 ```
![launch.json](https://s2.ax1x.com/2019/08/07/eoS25D.png)

----------


### 接着还是.vscode文件夹里创建一个名为[tasks.json](https://code.visualstudio.com/docs/editor/tasks#vscode)的文件 
然后输入以下代码(以下配置皆为VSCode默认生成的模板)
```
{
// 有关 tasks.json 格式的文档，请参见
    // https://go.microsoft.com/fwlink/?LinkId=733558
    "version": "2.0.0",
    "tasks": [
        {
            "type": "shell",
            "label": "gcc build",
            "command": "C:/mingw64/bin/gcc.exe",    //这行的地址改为gcc的地址
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "C:/mingw64/bin"     //这行的地址改为mingw64下的bin地址
            },
            "problemMatcher": [
                "$gcc"
            ]
        }
    ]
}
```


![tasks.json](https://s2.ax1x.com/2019/08/07/eoSgUO.png)


----------


# 测试编译和调试功能 
新建一个.c文件并在里面输入一些代码 比如helloword
``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int i;
    for (i = 0; i < 10; i++)
        printf("%d\n", i);
    system("pause");
    return 0;
}
```

![编译示图](https://s2.ax1x.com/2019/08/07/eo9oAf.png)
编译
![调试示图](https://s2.ax1x.com/2019/08/07/eo974S.png)
调试

我把我的工作区压缩包和Mingw-w64压缩包放到了下面这个链接

https://www.lanzous.com/b859892

----------





# 至此，教程结束！

