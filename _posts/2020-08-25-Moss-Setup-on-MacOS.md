---
layout:     post
title:      Moss Setup on MacOS
date:       2020-08-25
summary:    Steps to setup Moss (a system for detecting software similarity) on MacOS
categories: Text Moss Software
---

## Installation

1. Registering Moss at [here](http://theory.stanford.edu/~aiken/moss/) to  download it.

    ~~或者从[百度云](https://pan.baidu.com/s/123qmK_OIgyQZaZBVvGN_zw)下载呀, 密码是u22g~~

2. After sucessfully downloaded Moss, save name as `moss.pl` and move it to **Applications** folder.

    ![lLaAQir4NqEydU7](https://i.loli.net/2020/08/25/lLaAQir4NqEydU7.png)

3. Open terminal's configuration file.
    - if you are using zsh, type the following text in terminal
        ```
        open ~/.zshrc
        ```
    - if you are using bash, type the following text in terminal
        ```
        open ~/.bashrc
        ```

4. Add the following text at the bottom of the file.
    ```
    alias moss="/Applications/moss.pl"
    ```

    ![Pjew8uhcDoUW4ZE](https://i.loli.net/2020/08/25/Pjew8uhcDoUW4ZE.png)

5. Restart the terminal or type `source ~/.zshrc` in terminal to activate new alias.

6. Type `chmod +x /Applications/moss.pl` to activate Moss.

## Usage

1. Use `cd` to change directory where files to compare are located.

2. Type command in terminal according to your conditions.

    ```
    moss [-l language] [-d] [-b basefile1] ... [-b basefilen] [-m #] [-c "string"] file1 file2 file3 ...
    ```

    - Compare two c program `abc.c` and `xyz.c`
        ```
        moss -l c abc.c xyz.c
        ```

    - Compare all the c program and h program in two folders `folder1` and `folder2`.
        ```
        moss -d folder1/*.c folder1/*.h folder2/*.c folder2/*.h
        ```

    - Compare all the c program in two directory `dir1/*` and `dir2/*`, where `dir1/example.c` and `dir2/example.c` contains the base files.
        ```
        moss -l c -b dir1/example.c -b dir2/example.c -d dir1/*.c dir2/*.c
        ```

3. Copy the link to browser, then you will see the result.

    ![mlG8BjJ342gCOdk](https://i.loli.net/2020/08/25/mlG8BjJ342gCOdk.png)

4. Click on the file name, you will see more information.

    ![YkcV1j7h9OzgDA5](https://i.loli.net/2020/08/25/YkcV1j7h9OzgDA5.png)




| Line | Assumptions | Formula     | Justification            | References     |
| ---- | ----------- | ----------- | ------------------------ | -------------- |
| 1 | 1 | $B$ | Assump. I |  |
| 2 | 2 | $A$ | Assump. I |  |
| 3 | 1,2 | $(A \land B)$ | $ \land $I | 1,2 |
| 4 | 1,2 | $B$ | $ \land $E | 3 |
| 5 | 1 | $(A \rightarrow B)$ | $ \rightarrow $I | 2,4 |
