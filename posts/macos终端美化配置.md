# macos 终端美化配置

美化后的效果如图

![iterm2](../otherImages/item2.jpg)

1. 安装`iTerm2` 访问[此链接](https://iterm2.com/)进行下载安装

2. 打开`iTerm2` 在其中输入以下命令，以安装`brew`

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

安装好后，按照提示进行简单的配置操作。如果上面的命令失效，访问[brew官网](https://brew.sh/)

安装git:

```shell
brew install git
```

3. 手动安装`oh-my-zsh`

**从git上把oh-my-zsh clone下来到根目录下**

```shell
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
```

**再在根目录下copy一份.zshrc配置**

```shell
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```

4. 安装`powerlevel10k`使用码云的资源链接

```shell
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

5. 安装命令颜色高亮
```shell
brew install zsh-syntax-highlighting
```

6. 改写```.zshrc```配置

如下所示，在根目录下的etc文件夹下有一个zshrc文件，打开它复制如下的配置进行覆盖保存。

![ect](../otherImages/etc.jpg)

在终端输入

```shell
open .
```

就可以打开此目录。

将下面的配置粘贴进去进行覆盖保存。**记得修改其中的用户名**。

```shell
export ZSH="/Users/这里写你自己的mac用户名/.oh-my-zsh";
export PATH=/opt/local/bin:/opt/local/sbin:/Applications/xampp/xamppfiles/bin:$PATH

ZSH_THEME="powerlevel10k/powerlevel10k"

# command line 左邊想顯示的內容
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir dir_writable vcs vi_mode)# <= left prompt 設了 "dir"
# command line 右邊想顯示的內容
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status time) # <= right prompt 設了 "time"

POWERLEVEL9K_MODE='nerdfont-complete'

plugins=(git)

source $ZSH/oh-my-zsh.sh

```

7. 打开链接下载所需字体[字体文件](https://m.fontke.com/font/28278655/download/)
8. 安装使用字体

8.1 查询字体是否存在
```shell
brew search font
```
可以在`iTerm2`中使用 `command + f`快速查找
![font](../otherImages/font.jpg)

8.2 设置`tag`
```shell
brew tap homebrew/cask-fonts 
```

8.3 安装
```shell
brew install --cask font-sourcecodepro-nerd-font
```

9. 安装`zsh`
```shell
brew install zsh
```
设置`zsh`为默认
```shell
sudo sh -c "echo $(which zsh) >> /etc/shells" && chsh -s $(which zsh)
```

10. 设置主题颜色和字体

如下所示，打开`iTerm`进行操作
![set1](../otherImages/set1.jpg)

设置字体

![set2](../otherImages/set2.jpg)

设置颜色

![set3](../otherImages/set3.jpg)

最后将几个小模块的颜色，对应终端调整到对应的颜色即可。