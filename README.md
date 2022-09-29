# Setup Cheatsheet for MacOS

My personal preference only, skip when certain features do not appeal to you.

## SSH keys (for one GitHub account)

Setup SSH Key:

https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

## SSH keys (for multiple GitHub accounts)

Setup SSH Key:

https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

(If you are using two different accounts, consider one using `rsa` and the other using `ed25519` for easy identification)

Different SSH keys on same device:

https://www.freecodecamp.org/news/manage-multiple-github-accounts-the-ssh-way-2dadc30ccaca/

In file: `~/.ssh/config`

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

When cloning repos, use `git clone git@github.com:MainAccount/...` for main account and `git clone git@github.com-AltAccount:AltAccount/...` for alt account, note the extra `-AltAccount` for alt account.

**Remember to change `git config user.name` and  `git config user.email` also when using your alt account.**

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

These are the VS code plugins that I use, you can see if they are useful to you. These are the extension IDs, copy and paste them in the search extensions box to find them.
### Generally Useful

sdras.night-owl (A cooler theme)

johnpapa.vscode-peacock (Coloring of the VS code boundaries, to distinguish between different folders, e.g. to distinguish between the frontend and the backend of the project using different colour)

aaron-bond.better-comments (Coloring comments with //!, //TODO, //?)

bierner.markdown-preview-github-styles (Preview of .md files)

yzane.markdown-pdf (convert .md files into .pdf files)

mechatroner.rainbow-csv (Coloring of CSV files)

humao.rest-client (Create a .http file to make API requests)

adpyke.codesnap (Beautiful screenshots, suggest checking codesnap.transparentBackground)

mhutchie.git-graph (View Git history by Git Graph: view Git Graph (git log))

eamodio.gitlens (View more details about Git, e.g. when and who last edited a section of the code, sometimes useful sometimes a bit annoying)

### Language Specific

dan-c-underwood.arm (ARM Assembly Code, syntax highlighting)

Dart-Code.dart-code (Dart (used with Flutter), syntax highlighting, auto suggestions and more)

Dart-Code.flutter (Flutter, syntax highlighting, auto suggestions and more)

DigitalBrainstem.javascript-ejs-support (Javascript EJS, syntax highlighting)

golang.go (Go, syntax highlighting, auto suggestions, auto formatting and more)

justusadam.language-haskell (Haskell, syntax highlighting)

ms-python.python (Python, syntax highlighting)

scala-lang.scala (Scala, syntax highlighting)

<br />Prepared by KidProf