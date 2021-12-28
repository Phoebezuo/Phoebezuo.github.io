```
---
layout:     post
title:      Steps to change multiple commits
date:       2021-12-29
summary:    Steps to change contents on multiple git commits
categories: Git
---
```

1. According to this [repo](https://github.com/PotatoLabs/git-redate), type 

   ```
   brew tap PotatoLabs/homebrew-git-redate
   brew install git-redate
   ```

2. Look at your git history, determine how many commits you need to change.

   ![iShot2021-12-29 08.17.27](https://s2.loli.net/2021/12/29/8P7xfrXj6dIYnRG.png)

3. Run `git redate --commits [number of commits to view]` to open a VIM.

   ![iShot2021-12-28 23.30.39](https://s2.loli.net/2021/12/29/oEL51xPBcWkbw7d.png)

4. Type `i` to edit in VIM, then press `esc` and `:wq` after finish

   ![image-20211229082256523](https://s2.loli.net/2021/12/29/iKsdqoj5p7BYrRL.png)

5. Right now, the commits has been changed, use `git push` as normal. 