# 1.下载SFML以及Visual Studio 2022



（这个不教）

SFML官网链接:https://sfml-dev.org/index.php

Visual Studio 2022:https://visualstudio.microsoft.com/zh-hans/vs/



# 2.创建项目



![PixPin_2024-06-15_21-42-08](D:\word\md\pictures\PixPin_2024-06-15_21-42-08.png)

![PixPin_2024-06-15_21-42-48](D:\word\md\pictures\PixPin_2024-06-15_21-42-48.png)

![PixPin_2024-06-15_21-45-00](D:\word\md\pictures\PixPin_2024-06-15_21-45-00.png)



在新建的项目中，右键源文件添加一个项

![PixPin_2024-06-15_21-45-43](D:\word\md\pictures\PixPin_2024-06-15_21-45-43.png)

![PixPin_2024-06-15_21-46-13](D:\word\md\pictures\PixPin_2024-06-15_21-46-13.png)

![PixPin_2024-06-15_21-46-45](D:\word\md\pictures\PixPin_2024-06-15_21-46-45.png)



# 3.为项目添加库



右键项目名称，配置项目的属性

![PixPin_2024-06-15_21-48-25](D:\word\md\pictures\PixPin_2024-06-15_21-48-25.png)

![PixPin_2024-06-15_21-49-49](D:\word\md\pictures\PixPin_2024-06-15_21-49-49.png)



注意此时上方的配置和平台不要修改，初始状态就好

![PixPin_2024-06-15_21-50-57](D:\word\md\pictures\PixPin_2024-06-15_21-50-57.png)

在下载的SFML文件夹中找到include文件和lib文件

![PixPin_2024-06-15_21-53-02](D:\word\md\pictures\PixPin_2024-06-15_21-53-02.png)



![PixPin_2024-06-15_21-53-37](D:\word\md\pictures\PixPin_2024-06-15_21-53-37.png)

![PixPin_2024-06-15_21-54-46](D:\word\md\pictures\PixPin_2024-06-15_21-54-46.png)



# 4.配置项目的Debug和Release



先配置Debug，右边的下箭头是隐藏的，鼠标放上面就会显示了

![PixPin_2024-06-15_21-58-10](D:\word\md\pictures\PixPin_2024-06-15_21-58-10.png)

将下面的内容粘贴进去

**Debug：**

```
sfml-audio-d.lib
sfml-graphics-d.lib
sfml-system-d.lib
sfml-window-d.lib
sfml-network-d.lib
```

![PixPin_2024-06-15_21-58-33](D:\word\md\pictures\PixPin_2024-06-15_21-58-33.png)

将配置切换到Release，然后将下面的内容粘贴进去

**Release：**

```
sfml-audio.lib
sfml-graphics.lib
sfml-system.lib
sfml-window.lib
sfml-network.lib
```

![PixPin_2024-06-15_22-01-23](D:\word\md\pictures\PixPin_2024-06-15_22-01-23.png)



# 5.配置环境变量

**（部分人这一步之后就可以运行了）**

**（不能运行也不用慌，后面有解决办法）**



找到系统环境变量

![PixPin_2024-06-15_22-05-33](D:\word\md\pictures\PixPin_2024-06-15_22-05-33.png)

![PixPin_2024-06-15_22-05-53](D:\word\md\pictures\PixPin_2024-06-15_22-05-53.png)

**新建** **用户变量**

照着下图内容填就好

![PixPin_2024-06-15_22-06-42](D:\word\md\pictures\PixPin_2024-06-15_22-06-42.png)

![PixPin_2024-06-15_22-06-56](D:\word\md\pictures\PixPin_2024-06-15_22-06-56.png)



到这一步部分人就已经可以运行了

下面是一个示例代码：

```c++
#include <SFML/Graphics.hpp>
 
int main()
{
    sf::RenderWindow window(sf::VideoMode(200, 200), "SFML works!");
    sf::CircleShape shape(100.f);
    shape.setFillColor(sf::Color::Green);
 
    while (window.isOpen())
    {
        sf::Event event;
        while (window.pollEvent(event))
        {
            if (event.type == sf::Event::Closed)
                window.close();
        }
 
        window.clear();
        window.draw(shape);
        window.display();
    }
 
    return 0;
}
```

![PixPin_2024-06-15_22-24-12](D:\word\md\pictures\PixPin_2024-06-15_22-24-12.png)

（比较丑，没配置过）

运行成功的样子：

![PixPin_2024-06-15_22-24-25](D:\word\md\pictures\PixPin_2024-06-15_22-24-25.png)



# 6.添加运行文件(若5成功运行，略过即可)



找到SFML文件中的bin文件夹，复制其中所有的文件到项目中

![PixPin_2024-06-15_22-20-38](D:\word\md\pictures\PixPin_2024-06-15_22-20-38.png)

![PixPin_2024-06-15_22-21-18](D:\word\md\pictures\PixPin_2024-06-15_22-21-18.png)

（这里不直接移动是因为后面如果有用的话方便找）



沿着创建项目的路径找到cpp后缀文件所在的位置

![PixPin_2024-06-15_22-23-26](D:\word\md\pictures\PixPin_2024-06-15_22-23-26.png)

然后就可以运行了









# 附：

## 在项目中做游戏需要引入加载素材，素材文件夹放置的位置：

![PixPin_2024-06-15_22-51-15](D:\word\md\pictures\PixPin_2024-06-15_22-51-15.png)

上图fonts、graphics和sound文件夹就是我存放素材的位置，可以看到就是粘贴运行文件的位置







# 结尾：

本文所用到的教程：https://blog.csdn.net/Hsianus/article/details/130727463