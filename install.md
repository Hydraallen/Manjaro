# Manjaro
**Now, i'm using manjaro with KDE.**
## Arch (not in use)
[arch全教程](https://arch.icekylin.online/)
[arch美化](https://arch.icekylin.online/guide/advanced/beauty-1.html)

### Arch + Windows双系统
[教程](https://blog.linioi.com/posts/18/)  
[TheCW配制](https://www.bilibili.com/video/BV11J411a7Tp/?spm_id_from=333.999.0.0&vd_source=adf107bfee3c616e2040d1253b6e242c)  
[TheCW-Github](https://github.com/theniceboy) (.config) 

## Manjaro-gnome (not in use)
[系统配置](https://zhuanlan.zhihu.com/p/520119208)  
[安装软件](https://blog.csdn.net/loongfox/article/details/106048149)
[deepin-udis86安装](https://blog.51cto.com/u_15082397/4385511)

## Manjaro-KDE (in use)

### Manjaro + Windows双系统
[教程](https://zhuanlan.zhihu.com/p/376787855)
[系统配置](https://zhuanlan.zhihu.com/p/114296129)
[安装软件](https://www.cnblogs.com/xiaoyao404/p/16490685.html)

### 配置镜像源
```shell
sudo pacman-mirrors -i -c China -m rank
```

choose mirrors

```
sudo vi /etc/pacman.conf
```

Put the following at the end of this file
```
[archlinuxcn]
SigLevel = Optional TrustAll
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```

Then
```
sudo pacman -Syyu
sudo pacman -S archlinuxcn-keyring
```

If you cannot update, please try uninstall some old packages like `kdeconnect` etc(refer to the error message).

### clash for windows
`./cfw`

In system settings -> proxy:
use manually specified proxy configuration
```
HTTP Proxy:127.0.0.1
```

Exceptions: localhost, 127.0.0.0/8, ::1

**Reboot**

### bash to zsh
Check if zsh is installed
```
cat /etc/shells
chsh -s /bin/zsh
#有可能需要重启
echo $SHELL
```

#### Install oh-my-zsh
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

```
# 语法高亮插件(zsh-syntax-highlighting)
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting

# 自动补全插件(zsh-autosuggestions)
git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions

# 自动跳转插件(autojump)
brew install autojump
```
Refer to [zhihu](https://zhuanlan.zhihu.com/p/302883646)

### 包管理器
1. pacman
2. yay
3. paru (no need)
4. homebrew (useful but heavy)

安装方式
```
sudo pacman -S yay
yay -S google-chrome
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Remember to add the lines shown in terminal to .zshrc**

### Github
```
ssh-keygen -t rsa -C "xxx@xxx.com"
```












## 系统管理
 + 查看系统信息：`lsb_release -a `
 + 查看日志文件： `sudo du -t 100M /var journalctl --disk-usage `
 + 只保留近一周的日志，别的全部删除：`journalctl --vacuum-time=1w`
 + 删除指定日志文件：  
`sudo journalctl --vacuum-time=5d` 超过5天的日志自动删除  
`sudo journalctl --vacuum-size=500M` 超过500M的日志自动删除 
+ 进入root `sudo su -root`
+ 查看内存：`free -h`
+ 显示磁盘使用情况：`df -h`或者软件：filelight
+ `systemctl start dhcpcd` 启动服务  
+ `systemctl stop dhcpcd` 停止服务  
+ `systemctl restart dhcpcd` 重启服务  
+ `systemctl reload dhcpcd` 重新加载服务以及它的配置文件  
+ `systemctl status dhcpcd` 查看服务状态  
+ `systemctl enable dhcpcd` 设置开机启动服务  
+ `systemctl enable --now dhcpcd` 设置服务为开机启动并立即启动这个单元  
+ `systemctl disable dhcpcd` 取消开机自动启动  
+ `systemctl daemon-reload dhcpcd` 重新载入 systemd 配置。扫描新增或变更的服务单元、不会重新加载变更的配置
## 常用指令
`.` 代表当前目录  
`..` 代表当前目录的上级目录  
`cp ./a.py ./b.py` 复制命令：将当前路径下的 a.py 复制一份并命名为 b.py。`./` 代表当前文件夹所在路径，以此开头则为相对路径  
`cp -r ./a ./b` 复制整体文件夹  
`rm b.py` 删除命令。删除 b.py  
`rm -rf ./a` 删除整个文件夹  
`mv a.py b.py` 移动（重命名）命令。将 a.py 更名为 b.py

## Pacman
刷新本地镜像源:`sudo pacman -Sy `  
强制刷新本地镜像源:`pacman -Syy`  
进行全面系统更新(即通俗意义的“滚”):`sudo pacman -Syu`  
Pacman 在线安装软件的命令为 `pacman -S 软件包名字` 或者`yay -S 软件包名字`  
Pacman文件 `/etc/pacman.conf` 

### 安装软件
安装applemusic+snap：`https://snapcraft.io/install/apple-music-for-linux/arch`
`sudo pacman -S packagename` ： 安装指定软件  
`sudo pacman -Sy packagename` ： 刷新数据库后安装指定软件  
`sudo pacman -Sv packagename` ： 显示一些操作信息后安装指定软件  
`sudo pacman -U pkg.tar.xz` ：安装本地包  
`sudo pacman -U link.tar.xz` ：安装远程包
`yay -S com.qq.weixin.deepin`：安装微信

### 删除软件
`sudo pacman -R packagename` ：删除指定软件，保留其全部已经安装的依赖关系
`sudo pacman -Rs packagename` ：删除指定软件，并删除仅与该软件存在依赖关系的其他软件
`sudo pacman -Rsc packagename` ：删除指定软件，并删除所有与该软件存在依赖关系的其他软件
`sudo pacman -Rd packagename` ：删除指定软件，不检查依赖

### 搜索软件
`sudo pacman -Q`：显示所有软件  
`sudo pacman -Ss keyword`：在仓库中搜索含关键字的软件  
`sudo pacman -Qs keyword`：在已安装软件中搜索含关键词的软件  
`sudo pacman -Qi packagename`：搜索指定软件的详细信息   
`sudo pacman -Ql packagename`：列出指定软件的文件 

### 其他命令
`sudo pacman -Sw packagename`：只下载指定软件而不安装  
`sudo pacman -Sc` ：清理未安装的软件包  
`sudo pacman -Scc` ：清理所有的缓存文件  
所有自己安装的软件包: `pacman -Qe  `  
所有自己安装的软件包且不显示版本号: `pacman -Qeq `   
显示不再被依赖的包：`sudo pacman -Qdt`  
查找本机某一软件：`pacman -Qs xxx  `

### 安装微信
https://blog.csdn.net/weixin_39977764/article/details/125579302

## 键位修改
[参考](https://www.v2ex.com/t/875994)
### (X11)键位映射：
`~/.xmodmap`
### GNOME
[keyd](https://github.com/rvaiya/keyd)

## Clash
[教程](https://www.youtube.com/watch?v=EYNNTN_IWtU)  
[教程](https://www.jianshu.com/p/02e3e8ccfe80)
[设置](https://blog.linioi.com/posts/clash-on-arch/)

## 压缩包
`sudo pacman -S unarchiver`  
`unar xxx.zip`

## 仿MacOs：
[参考1](https://blog.51cto.com/u_15477117/5927174)  
[参考2](https://zhuanlan.zhihu.com/p/378627601)
## 清理缓存
### 清理pacman缓存包：
`sudo pacman -Rns $(pacman -Qtdq) `删除孤立软件包（常用）  
`sudo pacman -Sc ` 删除当前未安装的所有缓存包和未使用的同步数据库（可选）  
`sudo pacman -Scc` 从缓存中删除所有文件，这是最激进的方法，不会在缓存文件夹中留下任何内容（一般不使用）  
`paccache -r` 删除已安装和未安装包的所有缓存版本，但最近 3 个版本除外(自动执行paccache->见/etc/pacman.d/hooks/clean_package_cache.hook)  
### 清理yay缓存包：
`rm -rf ~/.cache/yay`

## Arch安装
https://zhuanlan.zhihu.com/p/596227524

## EndeavourOS安装
https://www.cnblogs.com/FanJPson/p/17028542.html
https://zhuanlan.zhihu.com/p/481032551
https://zhuanlan.zhihu.com/p/632567577

## i3wm
https://zhuanlan.zhihu.com/p/640577283


# Applications recommendation
## Input Method
> here we use fcitx5+rime
fcitx5 fcitx5-configtool fcitx5-qt fcitx5-gtk fcitx5-chinese-addons fcitx5-material-color fcitx5-rime

## zsh
zsh zsh-autosuggestions zsh-completions zsh-syntax-highlighting

## VPN
V2Ray

## Terminal
wezterm

## Terminal Applications
### Necessarities
git
vim
wget
curl

### Productivity
neovim
emacs
vscode

doomemacs
lunarvim

### helpful stuffs
ranger/joshuto
lazygit
lazynpm
autojump
unar
youtube-dl
ccat

### Toys
neofetch

## Browsers
Vivaldi (include Email)
Microsoft Edge/Chrome/Firefox

## packages
pip
python
npm
node
cargo
make 
git-lfs
gcc
g++

## font
> emoji
ttf-apple-emoji
> for GUI
ttf-ubuntu-font-family
> for tui symbols
ttf-nerd-fonts-symbols
> for coding
ttf-jetbrains-mono-nerd
> Maximum unicode coverage
ttf-unifont

## pdf reader
Zathura

## e-book reader
calibre

## Mathematics visualization tool
Geogebra

## Smart Capslock
xcape

## Awsome WM
[yoru](https://github.com/rxyhn/yoru)

WM: awesome
Compositor: picom
Application Launcher: rofi
Music Player ncmpcpp

