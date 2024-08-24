# zsh安装
```shell
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

vim ~/.zshrc

sudo apt install tmux cowsay
```
添加
```.zshrc
plugins=(vi-mode themes cp z tmux rand-quote command-not-found colored-man-pages history-substring-search git sudo zsh-syntax-highlighting zsh-autosuggestions)

quote | cowsay
bindkey '^P' history-search-backward
bindkey '^N' history-search-forward
```
刷新zsh配置文件
```shell
source ~/.zshrc
```
更换主题
```ZSH_THEME="powerlevel10k/powerlevel10k" in ~/.zshrc```

# 使用
## [vi-mode](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/vi-mode)

## [themes](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/themes)

## [z-command](https://github.com/agkozak/zsh-z)

