---
layout:     post
title:      Magma Setup on MacOS
date:       2020-08-24
summary:    Steps to setup Magma (a software package designed for computations in algebra, number theory, etc.) on MacOS
categories: Mathematics Magma Software
---

## Installation

1. Download Magma at [here](http://www.maths.usyd.edu.au/u/dhowden/loc/)

2. After sucessfully downloaded Magma, there is a folder appears in **Applications**
    ![mvw7Ve6IkYfbOKt](https://i.loli.net/2020/08/24/mvw7Ve6IkYfbOKt.png)

3. Open terminal's configuration file
    - if you are using zsh, type the following text in termial
    ```
    open ~/.zshrc
    ```
    - if you are using bash, type the following text in termial
    ```
    open ~/.bashrc
    ```

4. Add the following text at the bottom of the file
    ```
    alias magma="/Applications/Magma/magma"
    ```
    ![7gGM8PYXpjA6d59](https://i.loli.net/2020/08/24/7gGM8PYXpjA6d59.png)

5. Restart the terminal and using `cd` to change directory to current working directory

6. Type `magma` in your terminal, you will see something like this
    ![Z5GiJBDmnwXbc3F](https://i.loli.net/2020/08/24/Z5GiJBDmnwXbc3F.png)

7. To save your progression, type `SetLogFile("NameYouWant.log");` and then you will see a log file appears in current folder.
    ![vHIMu9poml4cJhN](https://i.loli.net/2020/08/24/vHIMu9poml4cJhN.png)
    ![s8owV7WpBckanqu](https://i.loli.net/2020/08/24/s8owV7WpBckanqu.png)
