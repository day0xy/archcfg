### 换源

 /etc/pacman.conf 

```
[archlinuxcn]
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
```

```
sudo pacman -Sy  archlinuxcn-keyring
```

blackarch

```
[blackarch]
Server = https://mirrors.ustc.edu.cn/blackarch/$repo/os/$arch
```

```
yay -S blackarch-keyring 
```



### 安装yay v2raya v2raya

```
sudo pacman -S yay v2ray v2raya downgrade
sudo systemctl enable --now v2raya.service
yay -S typora-free
```



### 导入数据

```
sudo pacman -S ntfs-3g
```

### 安装输入法

```
yay -S  fcitx5-im     fcitx5-chinese-addons fcitx5-pinyin-moegirl  fcitx5-pinyin-zhwiki
```

```
sudo vim /etc/environment

添加以下内容


GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
# burpsuite  字体模糊解决方法
_JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=on -Dswing.aatext=true'
```

### 基础软件安装

```
sudo pacman -S sof-firmware alsa-firmware alsa-ucm-conf
sudo pacman -S adobe-source-han-serif-cn-fonts nerd-fonts-complete
sudo pacman -S noto-fonts-cjk noto-fonts-emoji noto-fonts-extra 
yay -S chromium   google-chrome  
sudo pacman -S p7zip unrar unarchiver lzop lrzip 
yay -S virtualbox-ext-oracle  lx-music-desktop-bin gwenview spectacle kdenlive    

yay -S  obs-studio  okular kdeconnect icalingua++ jdk php php-cgi python-pip
yay -S docker vlc man zotero gimp openshot burpsuite

     

yay -S metasploit nmap sqlmap wireshark-qt ettercap-gtk  net-tools dsniff 010editor enum4linux  gobuster
yay -S dirb wfuzz arp-scan exploitdb  wpscan john  ffuf stegsolve stegseek steghide hashcat opencl-amd opencl-amd-dev partitionmanager sqlitebrowser  qbittorrent


yay -S vmware-workstation
sudo systemctl enable --now vmware-networks.service vmware-usbarbitrator.service
```



```
sudo usermod -a -G docker,wireshark,vboxusers day0xy
```

### 显卡驱动

amd核显

```
sudo pacman -S mesa lib32-mesa xf86-video-amdgpu vulkan-radeon lib32-vulkan-radeon libva-mesa-driver lib32-libva-mesa-driver mesa-vdpau lib32-mesa-vdpau
```

英伟达独显

```
sudo pacman -S nvidia nvidia-settings lib32-nvidia-utils
```

笔记本双显卡 另外安装

```
yay -S optimus-manager optimus-manager-qt
```



### zsh安装

```
yay -S zsh oh-my-zsh-git zsh-syntax-highlighting zsh-autosuggestions
chsh -s /bin/zsh
cp /usr/share/oh-my-zsh/zshrc ~/.zshrc
sudo ln -s /usr/share/zsh/plugins/zsh-syntax-highlighting /usr/share/oh-my-zsh/custom/plugins/
sudo ln -s /usr/share/zsh/plugins/zsh-autosuggestions /usr/share/oh-my-zsh/custom/plugins/
```



### git

```
git remote rm origin
git remote add origin git@github.com:DearjhonXXX9/archcfg.git
```

### lunarvim

```
去官网安装
```

### pip包

```
pip install -r
```



### 其他

#### 创建自启动脚本

```
1.创建一个启动service脚本

su

vim /usr/lib/systemd/system/rc-local.service

内容
----------------------------------------------------
[Unit]
Description="/etc/rc.local Compatibility"

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardInput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=multi-user.target
----------------------------------------------------
2.创建 /etc/rc.local 文件

vim /etc/rc.local
----------------------------------------------------
#!/bin/sh
# /etc/rc.local
if test -d /etc/rc.local.d; then
    for rcscript in /etc/rc.local.d/*.sh; do
        test -r "${rcscript}" && sh ${rcscript}
    done
    unset rcscript
fi
----------------------------------------------------
3.添加执行权限
chmod a+x /etc/rc.local

mkdir /etc/rc.local.d

systemctl enable rc-local

把sh脚本放在/etc/rc.local.d/文件夹中就行
```

#### kde wobbly window参数

```
less  15 78 8 
```



#### 触摸板设置

```
yay -S xf86-input-synaptics
```

```
sudoedit /etc/X11/xorg.conf.d/70-synaptics.conf
```



```
Section "InputClass"
        Identifier "touchpad catchall"
        Driver "synaptics"
        MatchIsTouchpad "on"

        Option "TapButton1" "1"            #单指敲击产生左键事件
        Option "TapButton2" "3"            #双指敲击产生中键事件

        Option "VertEdgeScroll" "on"       #滚动操作：横向、纵向、环形
        Option "VertTwoFingerScroll" "on"
        Option "VertScrollDelta"          "-111"	#natural scrolling
        Option "HorizScrollDelta"         "-111"
        Option "HorizEdgeScroll" "on"		
        Option "HorizTwoFingerScroll" "on"
        Option "CircularScrolling" "on"  
        Option "CircScrollTrigger" "2"

        Option "EmulateTwoFingerMinZ" "40" #精确度
        Option "EmulateTwoFingerMinW" "8"
        Option "CoastingSpeed" "20"        #触发快速滚动的滚动速度

        Option "PalmDetect" "1"            #避免手掌触发触摸板
        Option "PalmMinWidth" "3"          #认定为手掌的最小宽度
        Option "PalmMinZ" "200"            #认定为手掌的最小压力值
EndSection

```



logout
