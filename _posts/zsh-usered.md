---
title: 用zsh替换bash
date: 2019-08-03 00:22:06
tags: zsh
---
zsh貌似好看一点
先查看系统当前安装的shell

``` bash
cat /etc/shells
```

若未安装zsh
则通过软件源安装
debian下

``` bash
sudo apt-get install zsh
```

使用代码切换到zsh


``` bash
chsh -s /usr/bin/zsh
```

安装主题使它好看些


``` bash
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
source .zshrc
```

修改 ~/.zshrc 文件替换主题

```
ZSH_THEME="agnoster"
```

关于zsh的使用暂且告一段落了
