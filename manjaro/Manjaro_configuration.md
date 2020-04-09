配置manjaro
安装完成之后如果想使用顺畅还需要做一些配置，如更换国内镜像源、安装常用软件、美化主题等等。

1.更新国内镜像源

打开终端输入以下命令
sudo pacman-mirrors -i -c China -m rank

系统会针对国内的镜像进行测速并弹出选择窗口，选择一个最快的速率的国内源就行

这里推荐选择中国科技大学的镜像源
https://mirrors.ustc.edu.cn/manjaro



2.添加Archlinxucn的镜像源

打开终端输入
sudo gedit /etc/pacman.conf

在打开的文件末尾添加如下内容
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch


修改保存后更新缓存
sudo pacman -Syy

写入密钥
sudo pacman -S archlinuxcn-keyring

××××××××××××××××××××××××××××××××××××××××
如果在更新系统或者安装软件是如下错误
无法提交处理（无效或已损坏的软件包（PGP）签名）

那就再执行一遍

sudo pacman -S archlinuxcn-keyring
××××××××××××××××××××××××××××××××××××××××


3.更新系统
Manjaro是滚动更新的，每个一段时间就会更新一部分内容，所以在官网下载的系统包并不是最新的
安装完成后需要最好一下系统。
执行以下命令进行更新，该命令不但可以更新系统，也可以更新软件包。
sudo pacman -Syyu

当然你也可以直接运行manajor自带的软件包管理器，进行更新。


4.安装软件包
软件包通常有很多可选依赖，它们为软件提供额外功能， 并不强制要求安装它们。 安装软件时,pacman 将会输出它的可选依赖,当你想浏览已安装软件的可选依赖时可以使用pacman -Si得到关于可选依赖的简短描述。

安装或者升级软件包及其依赖：
pacman -S package_name1 package_name2 ...

软件包有多个版本（比如[extra]和[testing]），可以选择一个来安装：
pacman -S extra/package_name

用正则表达式安装多个软件包：
pacman -S $(pacman -Ssq package_regex)

===================================================================================

删除单个软件包，保留其全部已经安装的依赖关系
pacman -R package_name

删除指定软件包，及其所有没有被其他已安装软件包使用的依赖关系
pacman -Rs package_name

删除软件包和所有依赖这个软件包的程序
pacman -Rsc package_name

删除软件包，但是不删除依赖这个软件包的其他程序
pacman -Rdd package_name

====================================================================================

一个 pacman 命令就可以升级整个系统
pacman -Syu

====================================================================================

查询软件包

查询本地软件包数据库
pacman -Q

查询远程同步的数据库
pacman -S 

要查询已安装的软件包
pacman -Qs string1 string2 ...

罗列所有不再作为依赖的软件包
pacman -Qdt

=====================================================================================

清理软件包缓存
pacman 将下载的软件包保存在 /var/cache/pacman/pkg/ 并且不会自动移除旧的和未安装版本的软件包，因此需要手动清理，以免该文件夹过于庞大。

清除未安装软件包的缓存
pacman -Sc

删除近3个版本前的软件包
paccache -r

=====================================================================================

5.安装常用软件

安装输入法

安装fcitx-im的时候会搜索出4个包，直接按回车全部安装即可。
sudo pacman -S fcitx-googlepinyin
sudo pacman -S fcitx-im
sudo pacman -S fcitx-configtool


安装完成之后需要将fcitx加入到环境变量中才能激活输入法。
编辑配置文件：
sudo gedit ~/.xprofile
我使用的是gedit编辑器，也可以使用vim等其他编辑器
然后在文件里添加：
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
保存文件，重启系统。

重启系统后工具栏上会出现小键盘图标，右击图标配置当前输入法。



安装chrome浏览器
sudo pacman -S google-chrome

安装QQ：
sudo pacman -S deepin.com.qq.im

安装Tim
sudo pacman -S deepin.com.qq.office


安装WPS
安装主程序
sudo pacman -S wps-office

安装依赖字体
sudo pacman -S ttf-wps-fonts

安装Visual Studio Code
sudo pacman -S visual-studio-code-bin

安装Markdown编辑器
sudo pacman -S typora

安装微信
electronic-wechat是基于微信网页端的开源项目
安装electronic-wechat
sudo pacman -S electronic-wechat


********************************************************
安装deb包
有很多linux软件只提供.deb软件包，可以使用debtap将deb包转换成arch linxu包。

但是使用pacman -S debtap 安装Debtap时发现软件仓库里没有debtap。有可能是因为我之前将arch源换成了国内的镜像源，猜测可能是国内的镜像源中没有debtap包。

本人的解决方法是，使用其他包管理器来安装debtap，例如yaourt。
先安装yaourt管理工具
sudo pacman -S yaourt
然后再用yaourt来安装debtap
yaourt -S debtap
安装完成后升级debtap
sudo debtap -u
升级完毕之后就可以用debtap将deb包转换成pkg包了。

进入到deb包所在的目录，执行如下命令
sudo debtap package_name.deb
安装过程中会让输入 Package Name,这个name可以随便写。
会让输入license，填GPL。
命令执行完之后就会在.deb文件同级目录生成package_name.pkg.tar.xz软件包。
使用pacman安装本地包即可
sudo pacman -U package_name.pkg.tar.xz
