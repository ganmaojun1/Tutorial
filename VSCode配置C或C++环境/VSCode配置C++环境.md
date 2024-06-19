先放配置好的效果图：

![PixPin_2024-06-16_09-46-55](D:\word\md\pictures\PixPin_2024-06-16_09-46-55.png)



由于重新弄的话还是比较麻烦的，我就不拿全新的vscode进行演示了，请见谅。

如果实在觉得看起来有问题，可以结合结尾的主要参考教程。



# 1.下载VSCode



官网：https://code.visualstudio.com/

如果之前有安装过VSCode并进行过配置，只是简单卸载的话，再次安装之后还是会出现之前的配置信息

这里建议卸载干净之后再重新安装：

只需要将软件卸载之后，找到C盘的两个文件夹进行删除就好

- C:\Users\$ 用户名 \.vscode

- C:\Users\$ 用户名 \AppData\Roaming\Code

  【注】这里的 “$ 用户名” 根据自己的用户名而定。



# 2.设置中文环境



这一步其实是可有可无的，但是刚开始不熟悉的话，英文界面看着可能比较难受

![PixPin_2024-06-16_09-48-52](D:\word\md\pictures\PixPin_2024-06-16_09-48-52.png)

![PixPin_2024-06-16_09-49-21](D:\word\md\pictures\PixPin_2024-06-16_09-49-21.png)



# 3.安装 MinGW 编译器



安装编译器的话其实是有很多选择的

这里提供一个我认为很简单的方法——利用 MSYS2 进行安装



首先安装MSYS2

官网;https://www.msys2.org/

(注意安装路径，后面有用)



搜索关键词 vscode 以及 c++ 第一个结果就是我们所用到的教程

![PixPin_2024-06-16_09-53-56](D:\word\md\pictures\PixPin_2024-06-16_09-53-56.png)

往下拉找到安装示例

![PixPin_2024-06-16_10-00-31](D:\word\md\pictures\PixPin_2024-06-16_10-00-31.png)

具体过程就是：



1.打开Windows上的terminal，然后输入下面的命令

```
pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain
```

根据命令行显示的提示输入Yes（Y） or No (N),**这个教程下全部输入Y即可**



2.然后我们需要配置系统环境变量

![PixPin_2024-06-16_10-05-08](D:\word\md\pictures\PixPin_2024-06-16_10-05-08.png)

首先找到系统环境变量的配置页面

![PixPin_2024-06-15_22-05-33](D:\word\md\pictures\PixPin_2024-06-15_22-05-33-1718503572678-7.png)

![PixPin_2024-06-15_22-05-53](D:\word\md\pictures\PixPin_2024-06-15_22-05-53-1718503584268-12.png)



在用户变量中找到Path 然后点击编辑

![PixPin_2024-06-16_10-09-53](D:\word\md\pictures\PixPin_2024-06-16_10-09-53.png)



点击新建，然后粘贴MYSYS2中的bin文件夹路径

![PixPin_2024-06-16_10-11-30](D:\word\md\pictures\PixPin_2024-06-16_10-11-30.png)



这一步之后我们的编译器就算是安装完成了，可以打开terminal检查一下

按顺序输入下列命令

```
gcc --version
g++ --version
gdb --version
```

如果均正常显示的话那就没有问题，否则重新检查一下自己的Path是否正常配置



# 4.配置C/C++环境



在扩展中搜索c++进行下载

![PixPin_2024-06-16_09-56-17](D:\word\md\pictures\PixPin_2024-06-16_09-56-17.png)



然后我们提前新建一个空文件夹，到vscode中打开它

![PixPin_2024-06-16_10-20-21](D:\word\md\pictures\PixPin_2024-06-16_10-20-21.png)

然后点击刚刚新建的文件夹，这个时候应该是一片空白的。新建一个 cpp 后缀文件。

![PixPin_2024-06-16_10-22-14](D:\word\md\pictures\PixPin_2024-06-16_10-22-14.png)



打开新建的 cpp 文件，然后输入示例代码：

```c++
#include <iostream>

int main()
{
    std::cout << "Hello World！" << std::endl;
}
```

![PixPin_2024-06-16_10-25-14](D:\word\md\pictures\PixPin_2024-06-16_10-25-14.png)



接下来配置编译器路径：

按快捷键 Ctrl+Shift+P 调出命令面板，输入 C/C++，选择 “Edit Configurations (UI)” (英文版本)进入配置。

![PixPin_2024-06-16_10-28-27](D:\word\md\pictures\PixPin_2024-06-16_10-28-27.png)

这里配置两个选项：

1.编译器路径 

2.IntelliSense模式

![PixPin_2024-06-16_10-31-39](D:\word\md\pictures\PixPin_2024-06-16_10-31-39.png)



配置完成后 返回刚刚的页面，会发现多出了一个.vscode文件夹，并且里面有一个 c_cpp_properties.json 文件

![PixPin_2024-06-16_10-35-27](D:\word\md\pictures\PixPin_2024-06-16_10-35-27.png)

这里的配置内容，其实笔者也没有搞懂。读者若有兴趣自行阅读结尾处的两个参考教程

以下配置是我现在稳定运行的配置，但不保证不会出现问题。



在 c_cpp_properties.json 文件中粘贴以下内容

```
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "compilerPath": "D:/msys2/ucrt64/bin/g++.exe",
            "cStandard": "c17",
            "cppStandard": "c++20",
            "intelliSenseMode": "windows-gcc-x64"
        }
    ],
    "version": 4
}
```



接下来，创建一个 tasks.jason 文件来告诉vscode如何构建程序

按快捷键 Ctrl+Shift+P 调出命令面板，输入 tasks，选择 “Tasks:Configure Default Build Task”（英文界面）

![PixPin_2024-06-16_10-45-55](D:\word\md\pictures\PixPin_2024-06-16_10-45-55.png)

按照本教程进行配置的话，应该是能够看到下图所示的内容的。选择它即可。

（就算没有，最后还有简单方法）

（如果用其它方法安装的编译器也可以自行根据结尾参考文献进行配置）

![PixPin_2024-06-16_10-48-47](D:\word\md\pictures\PixPin_2024-06-16_10-48-47.png)

此时会出现一个名为 tasks.json 的配置文件

![PixPin_2024-06-16_10-54-57](D:\word\md\pictures\PixPin_2024-06-16_10-54-57.png)

如果不同也没关系，直接粘贴以下内容

```
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: g++.exe 生成活动文件",//任务的名字，可以自行更改
            "command": "D:/msys2/ucrt64/bin/g++.exe",
            "args": [//编译参数
                "-fdiagnostics-color=always",//颜色输出
                "-g",//生成调试信息
                "${file}",//当前文件
                "-o",//输出文件
                "${fileDirname}\\${fileBasenameNoExtension}.exe"//输出文件名
            ],
            "options": {
                "cwd": "D:/msys2/ucrt64/bin"//编译器所在目录
            },
            "problemMatcher": [
                "$gcc"//错误匹配
            ],
            "group": {
                "kind": "build",//表示该任务是构建任务
                "isDefault": true//表示快捷键 Ctrl+Shift+B 可以执行该任务
            },
            "detail": "编译器: D:/msys2/ucrt64/bin/g++.exe"//任务的详细信息
        }
    ]
}
```



接下来要在.vscode 文件夹中产生一个 launch.json 文件，用来配置调试的相关信息

一般教程都是让我们调试运行一下文件，让它生成这个 launch.json 文件，但是我发现这样经常失败

于是在本教程我们直接在 .vscode 文件夹中创建这个文件

![PixPin_2024-06-16_11-00-41](D:\word\md\pictures\PixPin_2024-06-16_11-00-41.png)

粘贴以下内容

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "g++.exe build active file",
            "preLaunchTask": "C/C++: g++.exe 生成活动文件",//调试前执行的任务，就是之前配置的tasks.json中的label字段
            "type": "cppdbg",//配置类型，只能为cppdbg
            "request": "launch",//请求配置类型，可以为launch（启动）或attach（附加）
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",//调试程序的路径名称
            "args": [],//调试传递参数
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,//true显示外置的控制台窗口，false显示内置终端
            "MIMode": "gdb",
            "miDebuggerPath": "",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```

然后我们就可以调试并运行我们的 cpp 文件了

（注意选择的任务名字）

![PixPin_2024-06-16_11-02-19](D:\word\md\pictures\PixPin_2024-06-16_11-02-19.png)



按照我们的配置，点击调试运行后会在终端输出

![PixPin_2024-06-16_11-04-19](D:\word\md\pictures\PixPin_2024-06-16_11-04-19.png)

（其实笔者这里有个问题。每次运行都会产生这个蓝色字。但是由于没啥影响，没做研究。）



**自此，我们的vscode c/c++运行环境就配置完成了！**



# 附

上面介绍的是运行环境的配置。其实对于vscode这个编辑器来说，运行环境是可以不要的，我们可以只把它当成一个文本编辑器。

作为一个文本编辑器，美观与方便使用自然是最重要的。

得益于vscode的强大社区，它拥有众多插件。其中有用来美化外观的，当然也有用来提高效率的。

这里为读者推荐一些笔者自用的插件（先只放图，之后有时间再详细介绍）：



1.官方发布的图标主题。建议安装，不仅是为了美观，同时也可以让文件更容易辨别

![PixPin_2024-06-16_11-19-19](D:\word\md\pictures\PixPin_2024-06-16_11-19-19.png)



2.我在用的一款切换背景的插件，还有很多其它的。第一张效果图就是利用这个插件实现的。

![PixPin_2024-06-16_11-17-11](D:\word\md\pictures\PixPin_2024-06-16_11-17-11.png)





3.可以方便的来修改命名，对于规范化编程来说很有帮助

![PixPin_2024-06-16_11-17-26](D:\word\md\pictures\PixPin_2024-06-16_11-17-26.png)





4.氛围感神器，不需要额外下载网易云音乐，直接就可以在vscode里听

![PixPin_2024-06-16_11-17-35](D:\word\md\pictures\PixPin_2024-06-16_11-17-35.png)



5.纠结变量应该取什么名字？这款插件可以解决你的问题，只需要输入关键词，就可以显示世界上其他人人是如何命名的

![PixPin_2024-06-16_11-17-47](D:\word\md\pictures\PixPin_2024-06-16_11-17-47.png)



6.代码截图神器，同样有很多版本，我选择这个版本的原因是可以选择左上角的三个小圆点，很像mac电脑，很有设计感

![PixPin_2024-06-16_11-17-58](D:\word\md\pictures\PixPin_2024-06-16_11-17-58.png)



7.实时检查代码的错误。但短时间内修改太快的话，会反应不过来。虽然这样，我也还没找到其它更好的

![PixPin_2024-06-16_11-18-11](D:\word\md\pictures\PixPin_2024-06-16_11-18-11.png)



8.AI助手，对于网上已经有的项目的话，比较方便，补全很准确。

![PixPin_2024-06-16_11-18-18](D:\word\md\pictures\PixPin_2024-06-16_11-18-18.png)



9.快捷键提示。当你多次用鼠标做一件重复的事时，会提示你这件事的快捷键是什么

![PixPin_2024-06-16_11-18-33](D:\word\md\pictures\PixPin_2024-06-16_11-18-33.png)



10.神器，必装。对于每次保存或运行的代码都会保存在本地，查看时还会高亮不同之处

![PixPin_2024-06-16_11-18-38](D:\word\md\pictures\PixPin_2024-06-16_11-18-38.png)



11.一键格式化（规范化）代码

![PixPin_2024-06-16_11-19-08](D:\word\md\pictures\PixPin_2024-06-16_11-19-08.png)



12.排序选中的文本或者数据

![PixPin_2024-06-16_11-19-14](D:\word\md\pictures\PixPin_2024-06-16_11-19-14.png)





13.这个主要是方便学习算法竞赛的选手。同时作为一个对比理想输出和实际输出的工具也是不错的。

但是太霸道了，开启后左侧任务栏会自动跳转到它的界面。

![PixPin_2024-06-16_11-19-25](D:\word\md\pictures\PixPin_2024-06-16_11-19-25.png)



未完待续，以后遇到好用的插件会继续更新。





# 结尾



**希望大家遇到问题不要气馁，多多尝试。加油！**



本教程主要参考教程：

1.https://code.visualstudio.com/docs/languages/cpp

2.https://zhuanlan.zhihu.com/p/87864677