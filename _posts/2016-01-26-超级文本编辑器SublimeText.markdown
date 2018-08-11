---
layout: post
title: 超级文本编辑器SublimeText
date: 2016-02-16 15:32:24.000000000 +09:00
---

----------

[TOC]


----------


# 简介

[Sublime Text3](http://www.sublimetext.com/)是一个超强的文本编辑工具，跨平台（Windows、Linux、Mac）；几乎你需要的功能都有，一切可修改（快捷键、插件包etc.）；界面优美；可惜的是不开源，不过即使不注册也可以使用。[Lime Text](http://limetext.org/)是其开源版的一种实现，我还没打算用这个。

- [12个不可不知的Sublime Text应用技巧和诀窍](https://segmentfault.com/a/1190000000505218);


# 基础插件

## Package-Control
顾名思义，[Package-Control](https://packagecontrol.io/)是包管理器，安装方法很简单，复制如下代码, 粘贴到Sublime的命令行窗口( "View --> Show Console" ), 回车即可, 参见官网：https://packagecontrol.io/installation#st3。

```
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

安装完成后，可按如下方式查看`Package Control`：
![调出Package Control](http://img.blog.csdn.net/20151126162103923)

## 中文乱码

有时打开含有中文的代码文件，会发现中文文字全部乱码，网上搜索了下，通过PackageControl安装了“**[ConvertToUTF-8](https://packagecontrol.io/packages/ConvertToUTF8)**” 和 Codecs33 ，重启Sublime Text就好了。

## Ubuntu下输入中文

下载并安装**sublime-text-imfix**包即可解决，终端命令如下：
```bash
sudo apt-get update && sudo apt-get upgrade
git clone https://github.com/lyfeyaj/sublime-text-imfix.git
cd sublime-text-imfix
./sublime-imfix
```
然后重启“Sublime Text3”即可，输入法不跟随光标依然无解，效果如下：

![Ubuntu下Sublime输入中文效果](http://img.blog.csdn.net/20160330205136469 "Ubuntu下Sublime输入中文效果")



## 输入法跟随光标

通过PackageControl安装“**[IMESupport](https://github.com/chikatoike/IMESupport)**”，重启Sublime Text3，即可解决：
![输入法跟随](http://img.blog.csdn.net/20160126230404701)

**注**：如项目自述，仅支持Windows。

## 在Sublime Text中运行脚本解释器

只需通过PackageControl安装“**[SublimeREPL](https://github.com/wuub/SublimeREPL)**”即可，官方文档[见此](http://sublimerepl.readthedocs.org/en/latest/)。然后设置好各解释器的系统环境变量`PATH`，注意Windows更改环境变量需要重启才能生效。

安装好后，使用<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>打开PackageControl，输入`repl`+`language`，然后选择语言即可。

下面是效果图：
![SublimeREPL:Lua效果图](http://img.blog.csdn.net/20160126235831443 "SublimeREPL: Sublime 中运行Lua解释器")

## 文件路径补全

最有效和好用的是**[AutoFileName](https://github.com/BoundInCode/AutoFileName)**插件，效果如下：

![AutoFileName文件路径补全插件效果](http://img.blog.csdn.net/20160311102513521 "AutoFileName文件路径补全插件效果")

## 表格编辑

**[Table Editor](https://github.com/vkocubinsky/SublimeTableEditor)**相当好用，安装好后参考自述文件（`Preferences --> Package Settings --> Table Editor --> README`），使用markdown预览查看用法，效果演示如下：

![TableEditor使用效果展示](http://img.blog.csdn.net/20160311201521507 "TableEditor使用效果展示")


## 语法高亮与着色

[SyntaxHighlightTools](https://packagecontrol.io/packages/SyntaxHighlightTools)为Sublime Text上的出色的语法着色插件.

## 代码匹配高亮

### Bracket Highlighter
安装: Package Control 搜索安装: `Bracket Highlighter`.
简介：可匹配 `[], (), {}, “”, ”, <tag></tag>`，高亮标记，便于查看起始和结束标记
使用：点击对应代码即可

## 代码布局

### Alignment

功能：”=”号对齐
简介：变量定义太多，长短不一，可一键对齐
使用：默认快捷键Ctrl+Alt+A和QQ截屏冲突，可设置其他快捷键如：Ctrl+Shift+Alt+A；先选择要对齐的文本


## 代码对比

### sublimerge

[sublimerge](http://www.sublimerge.com/), 从package control 搜索安装，或者下载后安装。

## 代码模板

可以使用 `SublimeTmpl` ，支持较多的语言，安装好后，自定义修改文件 ``Preference --> Package Settings --> SublimeTmpl --> Settings`` 的如下信息即可，创建 `py` 文件的快捷键： </kbd>Ctrl+Alt+Shift+P</kbd>

```jason
    "date_format" : "%Y-%m-%d %H:%M:%S",
    "attr": {
        "author": "Your Name",
        "email": "you@example.org",
        "link": "http://example.org"
    }
```


# 专用插件

## For Lua

只需要设置解释器路径即可。

### Windows
可以从[这里](http://www.dcc.ufrj.br/~fabiom/lua/lua52_win32.zip)下载Lua5.2解释器，解压后放到你想存放的位置，可以给其添加系统环境变量，不添加的话，可以配置绝对路径。

在Sublime Text中，`Tools -> Build System -> New Build System`，输入如下代码（注意替换你的Lua解释器路径，注意双斜杠），然后保存为“Lua.sublime-build”文件：

```
{
    "cmd": ["E:\\devtools\\lua52\\lua", "$file"], 
    "file_regex":"^(?:lua:)?[\t](...*?):([0-9]*):?([0-9]*)", 
    "selector":"source.lua" 

}
```

### Linux

```
{
    "cmd": ["lua", "$file"], 
    "file_regex":"^(?:lua:)?[\t](...*?):([0-9]*):?([0-9]*)", 
    "selector":"source.lua" 

}
```

如果你安装了**qlua**，那么你还可以用qlua来编译，跟上面一样新建构建配置文件，只需要把lua的路径替换成qlua所在路径即可，如下：

```
{
	"cmd": ["~/sfw/torch/install/bin/qlua", "$file"], 
	"file_regex":"^(?:lua:)?[\t](...*?):([0-9]*):?([0-9]*)", 
	"selector":"source.lua" 
}
```

这样就可以使用**image**包，显示图像了

```lua
require 'image';
img = image.load('/home/liu/data/256_ObjectCategories/056.dog/056_0044.jpg')
image.display(img)
```



### 自动补全

**LuaAutoComplete**好像有问题，安装后不起作用，**LuaSmartTips**很好用，也是通过Package Control安装。
![LuaSmartTips自动补全](http://img.blog.csdn.net/20160113101630533)


## For Python

最强大的是[JEDI](https://github.com/davidhalter/jedi)的**[SublimeJEDI](https://github.com/srusskih/SublimeJEDI)**，安装方法：

**SublimeJEDI**只是JEDI在Sublime Text中的插件，所以首先需要通过pip安装JEDI，命令：`sudo pip install jedi`

然后，可以通过PackageControl安装；或者下载[SublimeJEDI](https://github.com/srusskih/SublimeJEDI)源码，拷贝至Sublime Text包目录，并解压，重启Sublime即可； 或者在Linux下，可以通过以下命令安装：
```bash
cd ~/.config/sublime-text-2/Packages/
git clone https://github.com/srusskih/SublimeJEDI.git "Jedi - Python autocompletion"
```
如果想启用`.`作为补全触发器，需要通过`Preferences -> Package Settings -> LaTeXTools -> Settings-User`修改用户设置文件，加入如下代码：
```json
"auto_complete_triggers": [{"selector": "source.python", "characters": "."}],
```
效果图如下：
![JDEI Python 补全效果图](http://img.blog.csdn.net/20160330215835151 "JDEI Python 补全效果图")

## For Matlab

在Sublime Text中，`Tools -> Build System -> New Build System`，输入如下代码（注意替换你的MATLAB安装路径），然后保存为“MATLAB.sublime-build”文件：

```
{
	"cmd": ["E:/Program Files/MATLAB/R2014a/bin/matlab","-nosplash","-nodesktop","-r","$file_base_name"],"selector":"source.m"
}
```

输入如下测试代码，测试配置是否正确：

```MATLAB
a = zeros(2,1)
b = ones(2,1)
c = a + b
```

结果如下：
![Sublime Text 与MATLAB](http://img.blog.csdn.net/20160111104625028)


## For Markdown

### MarkdownEditing
支持Markdown语法高亮；支持Github Favored Markdown语法；自带3个主题。

更多查看：[Sublime插件：Markdown篇](http://www.jianshu.com/p/aa30cc25c91b)

### Markdown Extended

[Markdown Extended](https://github.com/jonschlinkert/sublime-markdown-extended)

### MarkdownLivePreview

<kbd>Alt+m</kbd>

### Markdown Preview
参见：[sublime text 2 下的Markdown写作](http://www.jianshu.com/p/378338f10263)


### OmniMarkupPreviewer

通过PackageControl或直接下载解压至Packages目录。 官网：[OmniMarkupPreviewer](http://theo.im/OmniMarkupPreviewer/ "官网")，下载地址：https://github.com/timonwong/OmniMarkupPreviewer

这个功能很强大哦，支持很多标记语言文档的预览，包括[reStructuredText](http://docutils.sourceforge.net/rst.html)，推荐使用。

**注**：如果你发现它不支持markdown目录的预览生成，那么不是它不行，是你没配置。复制`Preferences -> Package Settings -> OmniMarkupPreviewer -> Settings - Default` 中的内容到`Settings - Users`中，并在    // MarkdownRenderer options区域，即
    "renderer_options-MarkdownRenderer": 中添加`"toc"`，代码如下：

```json
        "extensions": ["tables", "strikeout", "fenced_code", "codehilite", "toc"]
```

然后通过<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>O</kbd>快捷键生成HTML预览，或者<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>X</kbd>导出。

## For reStructuredText

## 有用插件

- [reStructuredText]
- [OmniMarkupPreviewer](http://theo.im/OmniMarkupPreviewer/ "官网")，用于预览

### 编译Python项目文档

Python的项目文档，大都基于 `reStructuredText` 撰写， `Sphinx` 发布，如何在 Sublime 中，通过按 <kbd>Ctrl + B</kbd> 直接编译工程呢？很简单，点击 ``Tools --> Build System --> New Build System`` ，输入：

```
{
	"shell_cmd": "make html"
}

```

保存，打开你工程的 `Makefile` 文件，然后按 <kbd>Ctrl + Shift + B</kbd> 选择你刚才保存的那个名字，就可以自动编译成html文档了。



## For LaTex

关于LaTex排版，可以参考本人博客《LaTex排版一二三》

### Windows下基本环境配置

参考：[Making your first PDF with LaTeX and Sublime Text 2](http://economistry.com/2012/10/first-pdf-sublime-text-2-latex/)

需要安装三样东西

- [MiKTex](http://www.miktex.org/)或TeXLive（LaTex编译器，下载后直接安装就好）
- [LaTex Tools](https://packagecontrol.io/packages/LaTeXTools)（sublime text LaTex工具包，先在Sublime Text中安装Package Control，再用Package Control搜索安装LaTex Tools）或者[LaTeXing](http://www.latexing.com/features.html)（付费）
- [Sumatra PDF](http://www.sumatrapdfreader.org/free-pdf-reader.html)（预览PDF，与LaTex搭配的很好；此外还能查看epub、mobi、chm、xps、djvu格式）

#### 生成你的第一个LaTex文档

安装好“Sumatra PDF”，给系统添加**Sumatra PDF**安装路径环境变量，重启系统，在Sublime Tex中新建“.tex”文档，输入如下内容：

```latex
\documentclass{article}
  
\title{Title}
\author{Your Name}
  
\begin{document}
  
\maketitle{}
  
\section{Introduction}

This is where you will write your content. This is where you will write your content.This is where you will write your content.This is where you will write your content.

But how to write formulate? This is where you will write your content.This is where you will write your content.This is where ...

\section{Experiment}
  
\end{document}

```
按`Ctrl+B`应该会自动编译生成，如果没有，可能是编译的工具选择的不对，`Automatic`或`Latex`。

![编译后Sumatra PDF中预览效果](http://img.blog.csdn.net/20160111102631698)

#### 反向搜索
为了从PDF中定位到Latex源码位置，可设置Sumatra PDF的反向搜索命令（不设置默认用记事本notepad打开），在DOS命令窗口或者Sumatra PDF中选择`菜单-设置-选项`，找到设置反向搜索命令输入框（预览了PDF文件才会出现），输入：`"E:\Program Files\Sublime Text3 x64\sublime_text.exe" "%f:%l"`，请注意将路径替换为自己的Sublime Text 安装路径。

### Linux下环境配置

在Sublime中，通过`Preferences -> Package Settings -> LaTeXTools -> Settings-User`打开`LaTeXTools`的用户设置文件，找到如下代码，设置你的TeXLive安装路径：
```json
	"linux" : {
		// Path used when invoking tex & friends; MUST include $PATH
		"texpath" : "$PATH:～/sfw/TeXLive/2015/bin/x86_64-linux",
```

**注**：如果文档为中文文档，可能报错：“ctex-fontset-fandol.def:96:!!!!!”，这是因为PDF不支持中文，改用**xlatex**编译，在上述文件中设置编译引擎为：`	"builder": "traditional",`，并在文章开头加入`%!TEX program = xelatex`，即：
```latex
%!TEX program = xelatex
\documentclass[UTF8,10pt,oneside]{ctexbook}
```

### 字数统计

通过PackageControl安装“**LatexWordCount**”，然后按下图所示操作：
![LatexWordCount字数统计](http://img.blog.csdn.net/20160127210923294 "LatexWordCount字数统计")


### 自动补全

参考LatexTools的README文档（`Preference -> Package Settings -> LaTexTools -> REDME`），只需要安装“** LaTeX-cwl **”，效果如下图：
![LaTex命令自动补全](http://img.blog.csdn.net/20160228132246755 "LaTex命令自动补全(LaTeX-cwl)")

### 多文件编译

对于大型文档，通常使用$Latex$的`include, includeonly, input`等命令，那么在编写子文件时，如何通过按<kbd>Ctrl</kbd>+<kbd>B</kbd>就能直接编译，并且按<kbd>Ctrl</kbd>+<kbd>L</kbd>，<kbd>J</kbd>就能跳转到PDF中的相应位置呢？很简单，在你的**子文件第一行**加入如下代码（注意替换你的主文件名），然后编译即可：

```latex
%!TEX root = masterfilename.tex
```

### LaTex公式实时预览

偶然发现，LaTex公式可以实时预览了，当光标位于公式中时，就会在附近实时显示预览公式，不多说，上图：

![LaTeXTools新增公式实时预览功能](http://img.blog.csdn.net/20170224204150174?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZW5qb3l5bA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast "LaTeXTools新增公式实时预览功能")

猜着是 `LaTexTools` 的新特性，一看果然是：

![LaTexTools新特性](http://img.blog.csdn.net/20170224204815026?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZW5qb3l5bA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast "LaTexTools新特性")


# Sublime 设置

## 为Sublime Text 设置全局快捷键

1. 为Sublime Text创建快捷方式。找到Sublime Text安装目录中的“**sublime_text.exe**”文件，然后右击创建快捷方式，如下图：
![为Sublime Text创建快捷方式](http://img.blog.csdn.net/20160223091053234 "为Sublime Text创建快捷方式")

2. 为Sublime Tex设置全局快捷键。将上述快捷方式复制（或剪切）到Windows开始菜单目录：`C:\ProgramData\Microsoft\Windows\Start Menu\Programs`，然后右击快捷方式，在快捷键里输入快捷键，保存后即可，如下图：
![设置快捷键](http://img.blog.csdn.net/20160223091400989)

然后，就可以通过按 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>T</kbd> 启动Sublime Text ......


## 修改背景色

有些人喜欢背景色为**绿豆色**，那么Sublime Text也是可以修改的。

- 在你的安装目录中的“Packages”文件夹下，找到“Color Scheme - Default.sublime-package”文件，如下图：
![Color Scheme](http://img.blog.csdn.net/20160126173105044)

- 修改背景颜色值：用解压缩软件打开“Color Scheme - Default.sublime-package”文件，找到你使用的主题，如下图修改并保存（绿豆沙的RGB颜色值分别为：`199、237、204`，对应的16进制值：`#C7EDCC`）：
![编辑主题文件](http://img.blog.csdn.net/20160126173948119)
![修改为绿豆沙色](http://img.blog.csdn.net/20160126173546415)

- 修改效果：修改后的效果图如下
![修改后的效果](http://img.blog.csdn.net/20160126174116933 "修改后的效果图")

## 将Sublime Text添加至右键菜单

新建一个“右键菜单添加_Edit with Sublime Text3.bat”文件，复制（<kbd>Ctrl</kbd>+<kbd>C</kbd>）粘贴（<kbd>Ctrl</kbd>+<kbd>V</kbd>）如下代码，保存后，`右击` 该文件，选择 `以管理员身份运行`，提示成功后即可，注意修改你的Sublime Text安装路径。

```bat
@echo "Add to right click panel "Edit with Sublime Text3(&T)""

reg add "HKCR\*\shell\Sublime Text3(&T)" /ve /d "Edit with Sublime Text3"
reg add "HKCR\*\shell\Sublime Text3(&T)" /v Icon /t REG_SZ /d "E:\Program Files\Sublime Text3 x64\sublime_text.exe,0"
reg add "HKCR\*\shell\Sublime Text3(&T)\Command" /ve /d "E:\Program Files\Sublime Text3 x64\sublime_text.exe %%1"

pause
```
效果图如下：
![添加右键菜单：Edit with Sublime Text3](http://img.blog.csdn.net/20160126181137335 "右键菜单：Edit with Sublime Text3")

如果想删除这个右键菜单，DOS里输入如下命令（或新建bat文件，输入如下代码，右击以管理员身份运行），提示成功即可。

```bat
@echo "Delete right click panel "Edit with Sublime Text3(&T)""

reg delete "HKCR\*\shell\Sublime Text3(&T)"

pause
```

## 更改行间距

依次选择`Preferences -> setting - users`，在打开的设置文件中添加如下代码，根据自己喜好更改相应数值即可：
```jason
    // Additional spacing at the top of each line, in pixels
    "line_padding_top": 2,

    // Additional spacing at the bottom of each line, in pixels
    "line_padding_bottom": 2,
```

## 以十六进制查看修改文件

这个很简单，依次选择`File --> Reopen with encoding --> Hexadecimal`即可。

## 更改图标

不仅主题可以更换，图标也可以。在 Dribbble 上有大量重新设计的 Sublime Text 精美图标。更换方法参考 https://github.com/dbmzzo/Sublime-Text-2-Icon .


## 注册

```
—– BEGIN LICENSE —–  
TwitterInc  
200 User License  
EA7E-890007  
1D77F72E 390CDD93 4DCBA022 FAF60790  
61AA12C0 A37081C5 D0316412 4584D136  
94D7F7D4 95BC8C1C 527DA828 560BB037  
D1EDDD8C AE7B379F 50C9D69D B35179EF  
2FE898C4 8E4277A8 555CE714 E1FB0E43  
D5D52613 C3D12E98 BC49967F 7652EED2  
9D2D2E61 67610860 6D338B72 5CF95C69  
E36B85CC 84991F19 7575D828 470A92AB  
—— END LICENSE ——  
```



----------

[TOC]


