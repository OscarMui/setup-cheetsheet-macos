# Setup Cheatsheet for MacOS

My personal preference only, skip when certain features do not appeal to you.

## SSH keys (for one GitHub account)

Setup SSH Key:

https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

## SSH keys (for multiple GitHub accounts)

Setup SSH Key:

https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

(If you are using two different accounts, consider one using rsa and the other using ed25519)

Different SSH keys on same device:

https://www.freecodecamp.org/news/manage-multiple-github-accounts-the-ssh-way-2dadc30ccaca/

In file: ~/.ssh/config
```
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa

Host github.com-AltAccount
  AddKeysToAgent yes
  UseKeychain yes
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
```

When cloning repos, use `git clone git@github.com:MainAccount/...` for main account and `git clone git@github.com-AltAccount:AltAccount/...` for alt account.

REMEMBER TO CHANGE `git config user.name` and  `git config user.email` also.

## iterm 2
https://iterm2.com/

### Transparency
Preferences > Profiles > Window > Transparency

```
Opaque |++--------| Transparent
```

### Install color profile
https://github.com/MartinSeeler/iterm2-material-design

## oh my zsh
https://ohmyz.sh/

run `vim ~/.zshrc`

```
ZSH_THEME="ys"

plugins=(
	git
	zsh-autosuggestions
	web-search
)
```

### More on Plugins
git: Shortcuts for git commands

`gst`: `git status`

`gaa`: `git add --all`

`gcmsg`: `git commit -m`

`gp`: `git push`

`gl`: `git pull`

zsh-autosuggestions: make suggestions according to your recent history, tap right arrow to accept

web-search: use `google (keyword)`

### Show git username inside git repo (for multiple GitHub accounts)
run `code $ZSH_CUSTOM`

add this to `example.zsh`

```

YS_VCS_PROMPT_PREFIX1=" %{$reset_color%}on%{$fg[blue]%} "
YS_VCS_PROMPT_PREFIX2=":%{$fg[cyan]%}"


function git_prompt_info() {
  # If we are on a folder not tracked by git, get out.
  # Otherwise, check for hide-info at global and local repository level
  if ! __git_prompt_git rev-parse --git-dir &> /dev/null \
     || [[ "$(__git_prompt_git config --get oh-my-zsh.hide-info 2>/dev/null)" == 1 ]]; then
    return 0
  fi

  local ref
  ref=$(__git_prompt_git symbolic-ref --short HEAD 2> /dev/null) \
  || ref=$(__git_prompt_git rev-parse --short HEAD 2> /dev/null) \
  || return 0

  # Use global ZSH_THEME_GIT_SHOW_UPSTREAM=1 for including upstream remote info
  local upstream
  if (( ${+ZSH_THEME_GIT_SHOW_UPSTREAM} )); then
    upstream=$(__git_prompt_git rev-parse --abbrev-ref --symbolic-full-name "@{upstream}" 2>/dev/null) \
    && upstream=" -> ${upstream}"
  fi

  local gitprefix
  gitprefix="${YS_VCS_PROMPT_PREFIX1}git-$(git config user.name)${YS_VCS_PROMPT_PREFIX2}"

  echo "${gitprefix}${ref:gs/%/%%}${upstream:gs/%/%%}$(parse_git_dirty)${ZSH_THEME_GIT_PROMPT_SUFFIX}"
}
```

Now it would be showing `on git-username:master` instead of `on git:master`

## vim customisation
run `vim $HOME/.vimrc`

```
filetype plugin indent on
set term=xterm-256color
set number
syntax on
```

## TLDR
https://tldr.sh/ (Useful simplification of the help page of common commands)


## VS Code Plugins

### Generally Useful

sdras.night-owl (Theme)

johnpapa.vscode-peacock (Coloring of the VS code boundaries)

aaron-bond.better-comments (Coloring comments with //!, //TODO, //?)

bierner.markdown-preview-github-styles (Preview of .md files)

mechatroner.rainbow-csv (Coloring of CSV files)

humao.rest-client (Create a .http file to make API requests)

### Language Specific:

dan-c-underwood.arm (ARM Assembly Code)

Dart-Code.dart-code (Dart (used with Flutter))

Dart-Code.flutter (Flutter)

DigitalBrainstem.javascript-ejs-support (Javascript EJS)

golang.go (Go)

justusadam.language-haskell (Haskell)

ms-python.python (Python)

scala-lang.scala (Scala)

<br />Prepared by KidProf