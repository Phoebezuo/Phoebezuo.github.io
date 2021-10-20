---
layout:     post
title:      Borderlands2 Localisation on MacOS
date:       2021-10-20
summary:    Steps to setup Borderlands2 localisation on MacOS
categories: Mathematics Magma Software
---

1.   打开Borderlands2的steam页面

2.   `设置` -> `管理` -> `阅览本地文件`

     <img src="https://i.loli.net/2021/10/20/M5gBHWLxpGyjumf.png" alt="image-20211020122701704" style="zoom: 50%;" />

3.   在弹出的folder中，右键点击`Borderlands2.app`，之后选择`Show Package Contents`

     ![image-20211020122903108](https://i.loli.net/2021/10/20/2IOKDPwuXNQEohW.png)

4.   打开`Contents/GameData/`，可以看到`DLC`和`WillowGame` 这两个folder

     ![image-20211020123030711](https://i.loli.net/2021/10/20/IcEYn5La9UvpeNA.png)

5.   从这个[链接](https://drive.google.com/file/d/1IAPhkoUqXPyAUJ37PygSYYFEEpFK29uw/view?usp=sharing)上下载汉化补丁，可以看到有这些文件

     ![image-20211020123853711](https://i.loli.net/2021/10/20/BGJMjWRZXnm5A2E.png)

6.   先看`DLC`这个文件夹

     1.   如果游戏文件夹里也有`Compat/Localization/INT`这样的目录，则将汉化补丁的`INT`文件夹**直接覆盖游戏中对应的文件夹**
     2.   如果游戏文件夹里只有`Compat`文件夹，没有`Localization`文件夹，则将汉化补丁的`Localization`文件夹**直接复制到`Compat`文件夹中**

7.   之后看`WillowGame`这个文件夹

     1.   把汉化补丁中的`DefaultEngine.ini`覆盖到游戏文件`Config/`中去

          ![image-20211020125419580](https://i.loli.net/2021/10/20/6gMbHNcBxGy41oK.png)

     2.   将汉化补丁中的`CookedPCConsole/chFont.upk`和`CookedPCConsole/UI_Font_CN.upk`复制到游戏文件`CookedPCConsole`中去

     3.   将汉化补丁中的`Localization/INT`覆盖到游戏文件`Localization/INT`中去

在没有修改语言设置（原游戏语言为英语）的情况下，打开游戏就是中文。

