# archie

```
$ cd /opt
$ git clone https://github.com/doukeshi/archie.git
```

## Dotfiles

### dotrc

```
$ cp dotfiles/dotrc ~/.dotrc
```

### bash

```
# pacman -S bash-completion
$ cat ~/.bashrc
source $HOME/.dotrc
[[ -f $DOTFILE_HOME/shrc ]] && source $DOTFILE_HOME/shrc
```

### zsh

```
$ cat ~/.zshrc
source $HOME/.dotrc
ZSH_PLUGIN_HOME=/opt/archie/zplugins
[[ -f $DOTFILE_HOME/shrc ]] && source $DOTFILE_HOME/shrc
[[ -f $DOTFILE_HOME/zshrc ]] && source $DOTFILE_HOME/zshrc

$ cd /opt/zplugins
$ git clone https://github.com/rupa/z.git                                   --depth=1
$ git clone https://github.com/zsh-users/zsh-autosuggestions.git            --depth=1
$ git clone https://github.com/zsh-users/zsh-completions.git                --depth=1
$ git clone https://github.com/zsh-users/zsh-history-substring-search.git   --depth=1
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git        --depth=1
```

### vim

```
$ cat ~/.vimrc
source /usr/share/vim/vim82/vimrc_example.vim
if exists('$DOTFILE_HOME')
    source $DOTFILE_HOME/vimrc
endif
```

### git

Generate ~/.gitconfig

```
$ git config --global core.editor nvim
$ git config --global core.excludesfile ~/.gitignore_global
$ git config --global core.autocrlf input
$ git config --global user.name doukeshi
$ git config --global user.email doukeshi@users.noreply.github.com
$ git config --global user.signingkey 58B7C4175A06DDB5
$ git config --global commit.gpgsign true
$ git config --global pull.rebase true
```
