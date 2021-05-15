---
title: 基于PyQt5的BadUSB代码生成器
tags:
  - Python
  - PyQt5
categories: Python
cover: 'https://z3.ax1x.com/2020/12/09/r96Haj.jpg'
abbrlink: a2b2d8d2
date: 2021-04-22 12:07:00
---


## 软件界面介绍
主要是由两个widget(组件)组成的,基于mainwindow的支持MDI的仿文本文档窗口 和 基于widget的功能区组件
### 支持MDI的文本文档
这个文件规划的很完美 可以做一个独立的文件 可以继承使用 也就是ctrl+c和ctrl+v   (↓)

[![cLNMnS.jpg](https://z3.ax1x.com/2021/04/22/cLNMnS.jpg)](https://imgtu.com/i/cLNMnS)

这是主界面 本来是自己画UI的 完了 发现不好看 后来看到这个文本文档挺符合基本要求的 然后附加了一个MDI子窗口的功能

当然啊 现在还没有把所有功能给做出来  还有这个里面的子窗口也是一个widget 直接实例的一个对象 手写的一个TextEditUI

最值得一提的是 在切换子窗口的代码部分 我做了一个挺有意思 但很能会影响速度的操作   (↓)

[![cLNl7Q.jpg](https://z3.ax1x.com/2021/04/22/cLNl7Q.jpg)](https://imgtu.com/i/cLNl7Q)

我觉得 还有一点可以优化的是 上面的信号断开 应该可以断掉全部的信号 不是从act层面 而是从子窗口的视角来断开信号

### 附加的功能区组件

[![cLNuX8.jpg](https://z3.ax1x.com/2021/04/22/cLNuX8.jpg)](https://imgtu.com/i/cLNuX8)

这是主界面   按键识别框是一个QKeySequenceEdit组件 我本来也是手写了一个的(没发现QtDesigner居然自带了一个) 不过逻辑代码太多太多 在重构软件之后就用了这个方便一点的

打印字符串 和 sleep 都是两个简单的LineEdit

Ducky转换使用的GitHub大佬的  我给改成了一个函数 原项目地址: https://github.com/toxydose/Duckyspark

右边的两个箭头 可以调出层叠界面 是用来直接开启一个badusb代码示例的 (↓)

[![cLNQ0g.jpg](https://z3.ax1x.com/2021/04/22/cLNQ0g.jpg)](https://imgtu.com/i/cLNQ0g)

还有这个点击选择输入也有一个独立窗口的 (↓)

[![cLNn6f.jpg](https://z3.ax1x.com/2021/04/22/cLNn6f.jpg)](https://imgtu.com/i/cLNn6f)

这是初始的样子 点击其他按键后会显示所有的按键 (↓)

[![cLN3kj.jpg](https://z3.ax1x.com/2021/04/22/cLN3kj.jpg)](https://imgtu.com/i/cLN3kj)

所有的 按键按钮 都连接了一个指定信号 可以把按钮名字给打印到当前界面上方的LineEdit上 用的是find children方法 循环查找所有小孩 然后排除 “添加”，“清空”，”其它按键“这三个不需要映射的按钮

## 使用方法及Digi规范

软件界面还是挺简单直观的 想说一下咱们Digi开发板和Ducky的不同之处

我在软件开启时默认加载了一个Digi的头文件 想以此说明使用方法 后期也会做个检测 只有前三次开启时才会加载头文件 以后就放在层叠界面中

想看的时候再手动打开 头文件原项目地址: https://github.com/BesoBerlin/DigiKeyboard_DE/blob/master/DigiKeyboard.h

主要想介绍两个函数的使用 准确来时是四个   分别是

### sendKeyStroke
```
//sendKeyStroke: sends a key press AND release
void sendKeyStroke(byte keyStroke) {
```

这里的 keystroke 参数指的是 这样的数值  (↓)

```
#define KEY_A       4
#define KEY_B       5
#define KEY_F11     68
#define KEY_F12     69
#define KEY_TAB	    43
#define KEY_SPACE   44
```

```
//sendKeyStroke: sends a key press AND release with modifiers
void sendKeyStroke(byte keyStroke, byte modifiers) {
```

这里的 modifiers 就和 keystroke不一样了 它是这样的  (↓)

```
#define MOD_CONTROL_LEFT    (1<<0)
#define MOD_SHIFT_LEFT      (1<<1)
#define MOD_ALT_LEFT        (1<<2)
#define MOD_GUI_LEFT        (1<<3)
#define MOD_CONTROL_RIGHT   (1<<4)
#define MOD_SHIFT_RIGHT     (1<<5)
#define MOD_ALT_RIGHT       (1<<6)
#define MOD_GUI_RIGHT       (1<<7)
```

这是全部的修饰按键了 也就是上面按键组合只能是

```
​sendKeyStroke(KEY_A,MOD_CONTROL_LEFT）
​sendKeyStroke(KEY_F11,MOD_ALT_LEFT）
```

这种 而不能像下面这样 用两个普通的keystroke

    sendKeyStroke(KEY_E,KEY_ENTER)




----


### sendKeyPress
```
//sendKeyPress: sends a key press only - no release
//to release the key, send again with keyPress=0
void sendKeyPress(byte keyPress) {
```

```
//sendKeyPress: sends a key press only, with modifiers - no release
//to release the key, send again with keyPress=0
void sendKeyPress(byte keyPress, byte modifiers) {
```

参数的操作上面已经说过了 主要说下这个按下不松开 松开需要带着keypress参数为0 再发送一遍 是个什么操作

有两点 1.按下什么时候松开 2.能不能和其他按键组合按下 做成组合按键 举两个例子应该就能搞清楚了

    // 这是一直按下不松开
    sendKeyPress(KEY_A)

    // 按下并立即松开
    sendKeyPress(KEY_A,MOD_CONTROL_LEFT)
    sendKeyPress(0)

    // 按下2秒后再松开
    sendKeyPress(KEY_A)
    delay(2000)
    sendKeyPress(0)

    // 也可以不发送0参数 直接输入下一个按键函数就行了
    // 但不确定这样会不会有其他问题
    sendKeyPress(KEY_A)
    delay(2000)
    sendKeyPress(KEY_E,MOD_GUI_LEFT)

接下来举两个组合按键的例子

    sendKeyPress(KEY_E)
    sendKeyPress(MOD_GUI_LEFT)
    sendKeyPress(0)
    // 这样就解决了 sendKeyStroke只能一个普通按键一个修饰按键的短板了
    // 还有下面这个例子
    sendKeyPress(KEY_1)
    sendKeyPress(MOD_SHIFT_LEFT)
    sendKeyPress(0)
    // 按下上档键和主键盘数字按键 这样就可以不用print函数就能输出符号了
