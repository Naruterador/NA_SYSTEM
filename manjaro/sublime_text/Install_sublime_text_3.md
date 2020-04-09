###linux环境下安装sublime text3解压缩版

到官网下载压缩包
https://www.sublimetext.com/

使用cd命令到下载目录

将压缩包移动到/opt/目录下(注意你自己的压缩包的名字)
sudo mv sublime_text_3_build_3211_x64.tar.bz2 /opt/

你自己移动到/opt下

进行解压缩
sudo tar -jxvf 文件名.tar.bz2

修改解压缩后的文件名,因为启动器的执行路径和解压后的文件名不同
sudo mv sublime_text_3 sublime_text

使用vi查看启动器的配置信息
注意第7行的Exec的路径,如果之前没有修改目录名就会找不到这个文件

[Desktop Entry]
Version=1.0
Type=Application
Name=Sublime Text
GenericName=Text Editor
Comment=Sophisticated text editor for code, markup and prose
Exec=/opt/sublime_text/sublime_text %F
Terminal=false
MimeType=text/plain;
Icon=sublime-text
Categories=TextEditor;Development;
StartupNotify=true
Actions=Window;Document;

[Desktop Action Window]
Name=New Window
Exec=/opt/sublime_text/sublime_text -n
OnlyShowIn=Unity;

[Desktop Action Document]
Name=New File
Exec=/opt/sublime_text/sublime_text --command new_file
OnlyShowIn=Unity;



测试是否成功,运行sublime _text文件,注意不是那个sublime_text.desktop文件
若成功,在运行sublime_text.destop文件
都没问题的话将sublime_text.desktop移动到应用程序目录下
sudo mv sublime_text.desktop /usr/share/applications/
接下来就能通过快捷方式启动了
