###插件安装集合

使用Package Control组件安装
也可以安装package control组件，然后直接在线安装：

按Ctrl+ `(此符号为tab按键上面的按键) 调出console（注：避免热键冲突）
粘贴以下代码到命令行并回车：

import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())

如果在Perferences->中看到package control这一项，则安装成功。

用Package Control安装插件的方法：
按下Ctrl+Shift+P调出命令面板
输入install 调出 Install Package 选项并回车，然后在列表中选中要安装的插件。
方法介绍完了，接下来进入今天正题，一些有用的Sublime Text 3插件：

注意：安装插件时保持网络畅通，避免插件由于网络原因奔溃



1. Emmet（原名 Zen Coding）
一种快速编写html/css的方法

注意：安装Emmet的同时，也会自动安装其依赖PyV8 binary库，安装PyV8库会用较长时间，可以在Sublime左下角看到安装进程状态

2. html5
支持hmtl5规范的插件包

注意：与Emmet插件配合使用，效果更好

使用方法：新建html文档>输入html5>敲击Tab键>自动补全html5规范文档

3. jQuery
支持JQuery规范的插件包

4. javascript-API-Completions
支持Javascript、JQuery、Twitter Bootstrap框架、HTML5标签属性提示的插件，是少数支持sublime text 3的后缀提示的插件，HTML5标签提示sublime text 3自带，不过JQuery提示还是很有用处的，也可设置要提示的语言。

安装方法（请阅读链接详情）：http://www.ithao123.cn/content-10545789.html

5. JSFormat
JS代码格式化插件。

使用方法：使用快捷键ctrl+alt+f

6. SublimeLinter
一个支持lint语法的插件，可以高亮linter认为有错误的代码行，也支持高亮一些特别的注释，比如“TODO”，这样就可以被快速定位。（IntelliJ IDEA的TODO功能很赞，这个插件虽然比不上，但是也够用了吧）

7. BracketHighlighter

类似于代码匹配，可以匹配括号，引号等符号内的范围。

使用方法：系统默认为白色高亮，可以使用链接所述方法进行自定义配置

http://www.360doc.com/content/14/1111/15/15077656_424301780.shtml

8. Alignment
代码对齐，如写几个变量，选中这几行，Ctrl+Alt+A，哇，齐了。

9. Ctags
函数跳转，我的电脑上是Alt+点击 函数名称，会跳转到相应的函数

10. Doc​Blockr
注释插件，生成幽美的注释。标准的注释，包括函数名、参数、返回值等，并以多行显示，省去手动编写。

使用方法见：http://www.cnblogs.com/huangtailang/p/4499988.html

11. SideBarEnhancements
侧栏右键功能增强，非常实用
