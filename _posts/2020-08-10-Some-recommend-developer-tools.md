---
layout: post
title:  "Some recommend developer tools"
date:   2020-08-10
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

### Config Files

#### zshconfig

```
# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.
# if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
#   source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
# fi

# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH

# Path to your oh-my-zsh installation.
export ZSH="/Users/phoebezuo/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes


ZSH_THEME="agnoster"

# POWERLEVEL9K_MODE="nerdfont-complete"
# ZSH_THEME="powerlevel10k/powerlevel10k"


# Set list of themes to pick from when loading at random
# Setting this variable when ZSH_THEME=random will cause zsh to load
# a theme from this variable instead of looking in $ZSH/themes/
# If set to an empty array, this variable will have no effect.
# ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion.
# Case-sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"

# Uncomment the following line to disable bi-weekly auto-update checks.
# DISABLE_AUTO_UPDATE="true"

# Uncomment the following line to automatically update without prompting.
# DISABLE_UPDATE_PROMPT="true"

# Uncomment the following line to change how often to auto-update (in days).
# export UPDATE_ZSH_DAYS=13

# Uncomment the following line if pasting URLs and other text is messed up.
# DISABLE_MAGIC_FUNCTIONS="true"

# Uncomment the following line to disable colors in ls.
# DISABLE_LS_COLORS="true"

# Uncomment the following line to disable auto-setting terminal title.
# DISABLE_AUTO_TITLE="true"

# Uncomment the following line to enable command auto-correction.
ENABLE_CORRECTION="true"

# Uncomment the following line to display red dots whilst waiting for completion.
# COMPLETION_WAITING_DOTS="true"

# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# You can set one of the optional three formats:
# "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# or set a custom format using the strftime function format specifications,
# see 'man strftime' for details.
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
# Custom plugins may be added to $ZSH_CUSTOM/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(
    git
    zsh-syntax-highlighting
    zsh-autosuggestions
    jump
    zsh-completions
)

source $ZSH/oh-my-zsh.sh

# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
alias zshconfig="code ~/.zshrc"
alias themeconfig="code ~/.oh-my-zsh/themes/agnoster.zsh-theme"
alias code="open -a 'Visual Studio Code'"

#THIS MUST BE AT THE END OF THE FILE FOR SDKMAN TO WORK!!!
export SDKMAN_DIR="/Users/phoebezuo/.sdkman"
[[ -s "/Users/phoebezuo/.sdkman/bin/sdkman-init.sh" ]] && source "/Users/phoebezuo/.sdkman/bin/sdkman-init.sh"

export PATH=/usr/local/bin:$PATH

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
# [[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

```

#### themeconfig

```
# vim:ft=zsh ts=2 sw=2 sts=2
#
# agnoster's Theme - https://gist.github.com/3712874
# A Powerline-inspired theme for ZSH
#
# # README
#
# In order for this theme to render correctly, you will need a
# [Powerline-patched font](https://github.com/Lokaltog/powerline-fonts).
# Make sure you have a recent version: the code points that Powerline
# uses changed in 2012, and older versions will display incorrectly,
# in confusing ways.
#
# In addition, I recommend the
# [Solarized theme](https://github.com/altercation/solarized/) and, if you're
# using it on Mac OS X, [iTerm 2](https://iterm2.com/) over Terminal.app -
# it has significantly better color fidelity.
#
# If using with "light" variant of the Solarized color schema, set
# SOLARIZED_THEME variable to "light". If you don't specify, we'll assume
# you're using the "dark" variant.
#
# # Goals
#
# The aim of this theme is to only show you *relevant* information. Like most
# prompts, it will only show git information when in a git working directory.
# However, it goes a step further: everything from the current user and
# hostname to whether the last call exited with an error to whether background
# jobs are running in this shell will all be displayed automatically when
# appropriate.

### Segment drawing
# A few utility functions to make it easy and re-usable to draw segmented prompts

CURRENT_BG='NONE'

case ${SOLARIZED_THEME:-dark} in
    light) CURRENT_FG='white';;
    *)     CURRENT_FG='black';;
esac

# Special Powerline characters

() {
  local LC_ALL="" LC_CTYPE="en_US.UTF-8"
  # NOTE: This segment separator character is correct.  In 2012, Powerline changed
  # the code points they use for their special characters. This is the new code point.
  # If this is not working for you, you probably have an old version of the
  # Powerline-patched fonts installed. Download and install the new version.
  # Do not submit PRs to change this unless you have reviewed the Powerline code point
  # history and have new information.
  # This is defined using a Unicode escape sequence so it is unambiguously readable, regardless of
  # what font the user is viewing this source code in. Do not replace the
  # escape sequence with a single literal character.
  # Do not change this! Do not make it '\u2b80'; that is the old, wrong code point.
  SEGMENT_SEPARATOR=$'\ue0b0'
}

# Begin a segment
# Takes two arguments, background and foreground. Both can be omitted,
# rendering default background/foreground.
prompt_segment() {
  local bg fg
  [[ -n $1 ]] && bg="%K{$1}" || bg="%k"
  [[ -n $2 ]] && fg="%F{$2}" || fg="%f"
  if [[ $CURRENT_BG != 'NONE' && $1 != $CURRENT_BG ]]; then
    echo -n " %{$bg%F{$CURRENT_BG}%}$SEGMENT_SEPARATOR%{$fg%} "
  else
    echo -n "%{$bg%}%{$fg%} "
  fi
  CURRENT_BG=$1
  [[ -n $3 ]] && echo -n $3
}

# End the prompt, closing any open segments
prompt_end() {
  if [[ -n $CURRENT_BG ]]; then
    echo -n " %{%k%F{$CURRENT_BG}%}$SEGMENT_SEPARATOR"
  else
    echo -n "%{%k%}"
  fi
  echo -n "%{%f%}"
  CURRENT_BG=''
}

### Prompt components
# Each component will draw itself, and hide itself if no information needs to be shown

# Context: user@hostname (who am I and where am I)
prompt_context() {
  if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
    # prompt_segment black default "%(!.%{%F{yellow}%}.)%n@%m"
    prompt_segment black default "🔥"
  fi
}

# Git: branch/detached head, dirty status
prompt_git() {
  (( $+commands[git] )) || return
  if [[ "$(git config --get oh-my-zsh.hide-status 2>/dev/null)" = 1 ]]; then
    return
  fi
  local PL_BRANCH_CHAR
  () {
    local LC_ALL="" LC_CTYPE="en_US.UTF-8"
    PL_BRANCH_CHAR=$'\ue0a0'         # 
  }
  local ref dirty mode repo_path

  if [[ "$(git rev-parse --is-inside-work-tree 2>/dev/null)" = "true" ]]; then
    repo_path=$(git rev-parse --git-dir 2>/dev/null)
    dirty=$(parse_git_dirty)
    ref=$(git symbolic-ref HEAD 2> /dev/null) || ref="➦ $(git rev-parse --short HEAD 2> /dev/null)"
    if [[ -n $dirty ]]; then
      prompt_segment yellow black
    else
      prompt_segment green $CURRENT_FG
    fi

    if [[ -e "${repo_path}/BISECT_LOG" ]]; then
      mode=" <B>"
    elif [[ -e "${repo_path}/MERGE_HEAD" ]]; then
      mode=" >M<"
    elif [[ -e "${repo_path}/rebase" || -e "${repo_path}/rebase-apply" || -e "${repo_path}/rebase-merge" || -e "${repo_path}/../.dotest" ]]; then
      mode=" >R>"
    fi

    setopt promptsubst
    autoload -Uz vcs_info

    zstyle ':vcs_info:*' enable git
    zstyle ':vcs_info:*' get-revision true
    zstyle ':vcs_info:*' check-for-changes true
    zstyle ':vcs_info:*' stagedstr '✚'
    zstyle ':vcs_info:*' unstagedstr '●'
    zstyle ':vcs_info:*' formats ' %u%c'
    zstyle ':vcs_info:*' actionformats ' %u%c'
    vcs_info
    echo -n "${ref/refs\/heads\//$PL_BRANCH_CHAR }${vcs_info_msg_0_%% }${mode}"
  fi
}

prompt_bzr() {
  (( $+commands[bzr] )) || return

  # Test if bzr repository in directory hierarchy
  local dir="$PWD"
  while [[ ! -d "$dir/.bzr" ]]; do
    [[ "$dir" = "/" ]] && return
    dir="${dir:h}"
  done

  local bzr_status status_mod status_all revision
  if bzr_status=$(bzr status 2>&1); then
    status_mod=$(echo -n "$bzr_status" | head -n1 | grep "modified" | wc -m)
    status_all=$(echo -n "$bzr_status" | head -n1 | wc -m)
    revision=$(bzr log -r-1 --log-format line | cut -d: -f1)
    if [[ $status_mod -gt 0 ]] ; then
      prompt_segment yellow black "bzr@$revision ✚"
    else
      if [[ $status_all -gt 0 ]] ; then
        prompt_segment yellow black "bzr@$revision"
      else
        prompt_segment green black "bzr@$revision"
      fi
    fi
  fi
}

prompt_hg() {
  (( $+commands[hg] )) || return
  local rev st branch
  if $(hg id >/dev/null 2>&1); then
    if $(hg prompt >/dev/null 2>&1); then
      if [[ $(hg prompt "{status|unknown}") = "?" ]]; then
        # if files are not added
        prompt_segment red white
        st='±'
      elif [[ -n $(hg prompt "{status|modified}") ]]; then
        # if any modification
        prompt_segment yellow black
        st='±'
      else
        # if working copy is clean
        prompt_segment green $CURRENT_FG
      fi
      echo -n $(hg prompt "☿ {rev}@{branch}") $st
    else
      st=""
      rev=$(hg id -n 2>/dev/null | sed 's/[^-0-9]//g')
      branch=$(hg id -b 2>/dev/null)
      if `hg st | grep -q "^\?"`; then
        prompt_segment red black
        st='±'
      elif `hg st | grep -q "^[MA]"`; then
        prompt_segment yellow black
        st='±'
      else
        prompt_segment green $CURRENT_FG
      fi
      echo -n "☿ $rev@$branch" $st
    fi
  fi
}

# Dir: current working directory
prompt_dir() {
  prompt_segment blue $CURRENT_FG '%~'
  # prompt_segment blue black '%1~'
}

# Virtualenv: current working virtualenv
prompt_virtualenv() {
  local virtualenv_path="$VIRTUAL_ENV"
  if [[ -n $virtualenv_path && -n $VIRTUAL_ENV_DISABLE_PROMPT ]]; then
    prompt_segment blue black "(`basename $virtualenv_path`)"
  fi
}

# Status:
# - was there an error
# - am I root
# - are there background jobs?
prompt_status() {
  local -a symbols

  [[ $RETVAL -ne 0 ]] && symbols+="%{%F{red}%}✘"
  [[ $UID -eq 0 ]] && symbols+="%{%F{yellow}%}⚡"
  [[ $(jobs -l | wc -l) -gt 0 ]] && symbols+="%{%F{cyan}%}⚙"

  [[ -n "$symbols" ]] && prompt_segment black default "$symbols"
}

#AWS Profile:
# - display current AWS_PROFILE name
# - displays yellow on red if profile name contains 'production' or
#   ends in '-prod'
# - displays black on green otherwise
prompt_aws() {
  [[ -z "$AWS_PROFILE" ]] && return
  case "$AWS_PROFILE" in
    *-prod|*production*) prompt_segment red yellow  "AWS: $AWS_PROFILE" ;;
    *) prompt_segment green black "AWS: $AWS_PROFILE" ;;
  esac
}

## Main prompt
build_prompt() {
  RETVAL=$?
  prompt_status
  prompt_virtualenv
  prompt_aws
  prompt_context
  prompt_dir
  prompt_git
  prompt_bzr
  prompt_hg
  prompt_end
}

PROMPT='%{%f%b%k%}$(build_prompt) '
```

#### moss

```
#!/usr/bin/perl
#
# Please read all the comments down to the line that says "TOP".
# These comments are divided into three sections:
#
#     1. usage instructions
#     2. installation instructions
#     3. standard copyright
#
# Feel free to share this script with other instructors of programming
# classes, but please do not place the script in a publicly accessible
# place.  Comments, questions, and bug reports should be sent to
# moss-request@moss.stanford.edu.
#
# IMPORTANT: This script is known to work on Unix and on Windows using Cygwin.
# It is not known to work on other ways of using Perl under Windows.  If the
# script does not work for you under Windows, you can try the email-based
# version for Windows (available on the Moss home page).
#

#
#  Section 1. Usage instructions
#
#  moss [-l language] [-d] [-b basefile1] ... [-b basefilen] [-m #] [-c "string"] file1 file2 file3 ...
#
# The -l option specifies the source language of the tested programs.
# Moss supports many different languages; see the variable "languages" below for the
# full list.
#
# Example: Compare the lisp programs foo.lisp and bar.lisp:
#
#    moss -l lisp foo.lisp bar.lisp
#
#
# The -d option specifies that submissions are by directory, not by file.
# That is, files in a directory are taken to be part of the same program,
# and reported matches are organized accordingly by directory.
#
# Example: Compare the programs foo and bar, which consist of .c and .h
# files in the directories foo and bar respectively.
#
#    moss -d foo/*.c foo/*.h bar/*.c bar/*.h
#   
# Example: Each program consists of the *.c and *.h files in a directory under
# the directory "assignment1."
#
#    moss -d assignment1/*/*.h assignment1/*/*.c
#
#
# The -b option names a "base file".  Moss normally reports all code
# that matches in pairs of files.  When a base file is supplied,
# program code that also appears in the base file is not counted in matches.
# A typical base file will include, for example, the instructor-supplied
# code for an assignment.  Multiple -b options are allowed.  You should
# use a base file if it is convenient; base files improve results, but
# are not usually necessary for obtaining useful information.
#
# IMPORTANT: Unlike previous versions of moss, the -b option *always*
# takes a single filename, even if the -d option is also used.
#
# Examples:
#
#  Submit all of the C++ files in the current directory, using skeleton.cc
#  as the base file:
#
#    moss -l cc -b skeleton.cc *.cc
#
#  Submit all of the ML programs in directories asn1.96/* and asn1.97/*, where
#  asn1.97/instructor/example.ml and asn1.96/instructor/example.ml contain the base files.
#
#    moss -l ml -b asn1.97/instructor/example.ml -b asn1.96/instructor/example.ml -d asn1.97/*/*.ml asn1.96/*/*.ml
#
# The -m option sets the maximum number of times a given passage may appear
# before it is ignored.  A passage of code that appears in many programs
# is probably legitimate sharing and not the result of plagiarism.  With -m N,
# any passage appearing in more than N programs is treated as if it appeared in
# a base file (i.e., it is never reported).  Option -m can be used to control
# moss' sensitivity.  With -m 2, moss reports only passages that appear
# in exactly two programs.  If one expects many very similar solutions
# (e.g., the short first assignments typical of introductory programming
# courses) then using -m 3 or -m 4 is a good way to eliminate all but
# truly unusual matches between programs while still being able to detect
# 3-way or 4-way plagiarism.  With -m 1000000 (or any very
# large number), moss reports all matches, no matter how often they appear.  
# The -m setting is most useful for large assignments where one also a base file
# expected to hold all legitimately shared code.  The default for -m is 10.
#
# Examples:
#
#   moss -l pascal -m 2 *.pascal
#   moss -l cc -m 1000000 -b mycode.cc asn1/*.cc
#
#
# The -c option supplies a comment string that is attached to the generated
# report.  This option facilitates matching queries submitted with replies
# received, especially when several queries are submitted at once.
#
# Example:
#
#   moss -l scheme -c "Scheme programs" *.sch
#
# The -n option determines the number of matching files to show in the results.
# The default is 250.
#
# Example:
#   moss -c java -n 200 *.java
# The -x option sends queries to the current experimental version of the server.
# The experimental server has the most recent Moss features and is also usually
# less stable (read: may have more bugs).
#
# Example:
#
#   moss -x -l ml *.ml
#

#
# Section 2.  Installation instructions.
#     
# You may need to change the very first line of this script
# if perl is not in /usr/bin on your system.  Just replace /usr/bin
# with the pathname of the directory where perl resides.
#

#
#  3. Standard Copyright
#
#Copyright (c) 1997 The Regents of the University of California.
#All rights reserved.
#
#Permission to use, copy, modify, and distribute this software for any
#purpose, without fee, and without written agreement is hereby granted,
#provided that the above copyright notice and the following two
#paragraphs appear in all copies of this software.
#
#IN NO EVENT SHALL THE UNIVERSITY OF CALIFORNIA BE LIABLE TO ANY PARTY FOR
#DIRECT, INDIRECT, SPECIAL, INCIDENTAL, OR CONSEQUENTIAL DAMAGES ARISING OUT
#OF THE USE OF THIS SOFTWARE AND ITS DOCUMENTATION, EVEN IF THE UNIVERSITY OF
#CALIFORNIA HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#
#THE UNIVERSITY OF CALIFORNIA SPECIFICALLY DISCLAIMS ANY WARRANTIES,
#INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY
#AND FITNESS FOR A PARTICULAR PURPOSE.  THE SOFTWARE PROVIDED HEREUNDER IS
#ON AN "AS IS" BASIS, AND THE UNIVERSITY OF CALIFORNIA HAS NO OBLIGATION TO
#PROVIDE MAINTENANCE, SUPPORT, UPDATES, ENHANCEMENTS, OR MODIFICATIONS.
#
#
# STOP.  It should not be necessary to change anything below this line
# to use the script.
#
use IO::Socket;

#
# As of the date this script was written, the following languages were supported.  This script will work with
# languages added later however.  Check the moss website for the full list of supported languages.
#
@languages = ("c", "cc", "java", "ml", "pascal", "ada", "lisp", "scheme", "haskell", "fortran", "ascii", "vhdl", "perl", "matlab", "python", "mips", "prolog", "spice", "vb", "csharp", "modula2", "a8086", "javascript", "plsql", "verilog");

$server = 'moss.stanford.edu';
$port = '7690';
$noreq = "Request not sent.";
$usage = "usage: moss [-x] [-l language] [-d] [-b basefile1] ... [-b basefilen] [-m #] [-c \"string\"] file1 file2 file3 ...";

#
# The userid is used to authenticate your queries to the server; don't change it!
#
$userid=355863733;

#
# Process the command line options.  This is done in a non-standard
# way to allow multiple -b's.
#
$opt_l = "c";   # default language is c
$opt_m = 10;
$opt_d = 0;
$opt_x = 0;
$opt_c = "";
$opt_n = 250;
$bindex = 0;    # this becomes non-zero if we have any base files

while (@ARGV && ($_ = $ARGV[0]) =~ /^-(.)(.*)/) {
    ($first,$rest) = ($1,$2);

    shift(@ARGV);
    if ($first eq "d") {
	$opt_d = 1;
	next;
    }
    if ($first eq "b") {
	if($rest eq '') {
	    die "No argument for option -b.\n" unless @ARGV;
	    $rest = shift(@ARGV);
	}
	$opt_b[$bindex++] = $rest;
	next;
    }
    if ($first eq "l") {
	if ($rest eq '') {
	    die "No argument for option -l.\n" unless @ARGV;
	    $rest = shift(@ARGV);
	}
	$opt_l = $rest;
	next;
    }
    if ($first eq "m") {
	if($rest eq '') {
	    die "No argument for option -m.\n" unless @ARGV;
	    $rest = shift(@ARGV);
	}
	$opt_m = $rest;
	next;
    }
    if ($first eq "c") {
	if($rest eq '') {
	    die "No argument for option -c.\n" unless @ARGV;
	    $rest = shift(@ARGV);
	}
	$opt_c = $rest;
	next;
    }
    if ($first eq "n") {
	if($rest eq '') {
	    die "No argument for option -n.\n" unless @ARGV;
	    $rest = shift(@ARGV);
	}
	$opt_n = $rest;
	next;
    }
    if ($first eq "x") {
	$opt_x = 1;
	next;
    }
    #
    # Override the name of the server.  This is used for testing this script.
    #
    if ($first eq "s") {
	$server = shift(@ARGV);
	next;
    }
    #
    # Override the port.  This is used for testing this script.
    #
    if ($first eq "p") {
	$port = shift(@ARGV);
	next;
    }
    die "Unrecognized option -$first.  $usage\n";
}

#
# Check a bunch of things first to ensure that the
# script will be able to run to completion.
#

#
# Make sure all the argument files exist and are readable.
#
print "Checking files . . . \n";
$i = 0;
while($i < $bindex)
{
    die "Base file $opt_b[$i] does not exist. $noreq\n" unless -e "$opt_b[$i]";
    die "Base file $opt_b[$i] is not readable. $noreq\n" unless -r "$opt_b[$i]";
    die "Base file $opt_b is not a text file. $noreq\n" unless -T "$opt_b[$i]";
    $i++;
}
foreach $file (@ARGV)
{
    die "File $file does not exist. $noreq\n" unless -e "$file";
    die "File $file is not readable. $noreq\n" unless -r "$file";
    die "File $file is not a text file. $noreq\n" unless -T "$file";
}

if ("@ARGV" eq '') {
    die "No files submitted.\n $usage";
}
print "OK\n";

#
# Now the real processing begins.
#

$sock = new IO::Socket::INET (
                                  PeerAddr => $server,
                                  PeerPort => $port,
                                  Proto => 'tcp',
                                 );
die "Could not connect to server $server: $!\n" unless $sock;
$sock->autoflush(1);

sub read_from_server {
    $msg = <$sock>;
    print $msg;
}

sub upload_file {
    local ($file, $id, $lang) = @_;
#
# The stat function does not seem to give correct filesizes on windows, so
# we compute the size here via brute force.
#
    open(F,$file);
    $size = 0;
    while (<F>) {
	$size += length($_);
    }
    close(F);

    print "Uploading $file ...";
    open(F,$file);
    $file =~s/\s/\_/g;    # replace blanks in filename with underscores
    print $sock "file $id $lang $size $file\n";
    while (<F>) {
	print $sock $_;
    }
    close(F);
    print "done.\n";
}

print $sock "moss $userid\n";      # authenticate user
print $sock "directory $opt_d\n";
print $sock "X $opt_x\n";
print $sock "maxmatches $opt_m\n";
print $sock "show $opt_n\n";

#
# confirm that we have a supported languages
#
print $sock "language $opt_l\n";
$msg = <$sock>;
chop($msg);
if ($msg eq "no") {
    print $sock "end\n";
    die "Unrecognized language $opt_l.";
}

# upload any base files
$i = 0;
while($i < $bindex) {
    &upload_file($opt_b[$i++],0,$opt_l);
}

$setid = 1;
foreach $file (@ARGV) {
    &upload_file($file,$setid++,$opt_l);
}

print $sock "query 0 $opt_c\n";
print "Query submitted.  Waiting for the server's response.\n";
&read_from_server();
print $sock "end\n";
close($sock);
```
