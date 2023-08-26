# zsh安装
```shell
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions

vim ~/.zshrc
```
添加
```.zshrc
plugins=(git sudo zsh-syntax-highlighting zsh-autosuggestions)
```
刷新zsh配置文件
```shell
source ~/.zshrc
```

