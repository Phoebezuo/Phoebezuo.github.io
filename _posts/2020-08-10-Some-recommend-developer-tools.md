---
layout:  post
title:   Some recommend developer tools
date:    2020-08-10
summary: 记录一些编程软件的配置和插件
categories: MacOS Iterm Zsh
---

## [Visual Studio Code](https://code.visualstudio.com/download)

- 推荐指数：★★★★★
- 推荐理由：功能强大且轻巧的免费代码编辑器，里面有很多插件可以实现各种功能。

<div class="showcase">
  <img style="width:50%" src="/images/post/developer/vscode_1.gif" alt="">
</div>

| Plugins                                                      | Describe                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) | The goal of this spell checker is to help catch common spelling errors while keeping the number of false positive low. |
| [Code Time](https://marketplace.visualstudio.com/items?itemName=softwaredotcom.swdc-vscode) | Code Time is an open source plugin that provides programming metrics right in Visual Studio Code. |
| [Indent Rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow) | Makes indentation easier to read.                            |
| [Material Theme](https://marketplace.visualstudio.com/items?itemName=Equinusocio.vsc-material-theme) | The most epic theme now for Visual Studio Code.              |
| [Setting Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync) | Synchronize Settings, Snippets, Themes, File Icons, Launch, Keybindings, Workspaces and Extensions Across Multiple Machines Using GitHub Gist. |
| [TabNine](https://marketplace.visualstudio.com/items?itemName=TabNine.tabnine-vscode) | All-language autocompleter — TabNine uses machine learning to help you write code faster. |
| [TODO Highlight](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight) | Highlight TODOs, FIXMEs, and any keywords, annotations...    |
| [Waka Time](https://marketplace.visualstudio.com/items?itemName=WakaTime.vscode-wakatime) | Metrics, insights, and time tracking automatically generated from your programming activity. |

## [Iterm](https://www.iterm2.com/)

- 推荐指数：★★★★★
- 推荐理由：它比Mac自带的terminal功能强大很多，可以通过改变配色字体等改变颜值。如果下载了oh-my-zsh，还有更多pluging大大提升了效率。

<div class="showcase">
  <img style="width:50%" src="/images/post/developer/iterm_1.gif" alt="">
</div>

### Change Shell to ZSH

1. Install homebrew via xcode

   ```
   $ xcode-select —-install
   $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

2. Install zsh via homebrew and use the home-brew version of zsh

   ```
   $ brew install zsh
   $ chsh -s /usr/local/bin/zsh
   ```

3. Test if we are using the correct zsh

   ```
   $ echo $0
   zsh   //correct

   $ which zsh
   /usr/local/bin/zsh   //correct
   ```

4. Install oh-my-zsh

   ```
   $ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
   ```

### Change Themes and Install Fonts

1. Install Powerline fonts

   ```
   $ git clone https://github.com/powerline/fonts.git
   $ cd fonts
   $ ./install.sh
   ```

2. Change the Theme to "agnoster"

   ```
   $ open ~/.zshrc
   Set ZSH_THEME="agnoster" and save the file
   ```

3. Quit iTerm and reopen it

4. Add font in Iterm

   ```
   iTerm2 → Preferences → Profiles → Text → Change Font
   ```
   <div class="showcase">
     <img style="width:50%" src="/images/post/developer/font.png" alt="">
   </div>

### Customise Color Scheme

<div class="showcase">
  <img style="width:50%" src="/images/post/developer/color.png" alt="">
</div>

### Install Plugins

1. Install Syntax Highlighting plugin

   ```
   $ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   ```

2. Install ZSH-AutoSuggestion plugin

   ```
   $ git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
   ```

3. Edit in zshrc file

   ```
   $ open ~/.zshrc

   plugins=(
       git
       zsh-syntax-highlighting
       zsh-autosuggestions
       jump
   )
   ```

4. Activiate the zshrc file

   ```
   source ~/.zshrc
   ```

### Notes

1. Add alias in zshrc file

   ```
   alias zshconfig="code ~/.zshrc"
   alias themeconfig="code ~/.oh-my-zsh/themes/agnoster.zsh-theme"
   alias code="open -a 'Visual Studio Code'"
   ```

2. Change terminal title to emoji

   ```
   prompt_context() {
     if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
       prompt_segment black default "🔥"
     fi
   }
   ```

3. Click here to see zshconfig file.

4. Click here to see themeconfig file.

5. Trivial settings

  <div class="showcase">
    <img style="width:50%" src="/images/post/developer/setting.png" alt="">
  </div>
