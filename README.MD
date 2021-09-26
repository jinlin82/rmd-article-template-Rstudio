<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Rmarkdown article template](#rmarkdown-article-template)
    - [使用方法](#使用方法)
        - [软件要求](#软件要求)
        - [编译方法I：使用 Windows `发送到` 功能编译](#编译方法i：使用-windows-发送到-功能编译)
        - [编译方法II：在 Vscode 中编译](#编译方法ii：在-vscode-中编译)
        - [~~编译方法III：在 Rstudio 中编译（**有bug，不要使用**）~~](#编译方法iii：在-rstudio-中编译有bug不要使用)
    - [编译常见错误的原因及解决方法](#编译常见错误的原因及解决方法)
    - [RMD-ARTICLE-TEMPLATE介绍](#rmd-article-template介绍)
        - [项目文件结构](#项目文件结构)
    - [编辑修改方法](#编辑修改方法)
        - [如何运行 Rmarkdown 中的 python 代码](#如何运行-rmarkdown-中的-python-代码)
        - [rmd-template.rmd相关说明](#rmd-templatermd相关说明)
        - [rmd生成幻灯片beamer内容相关说明](#rmd生成幻灯片beamer内容相关说明)

<!-- markdown-toc end -->

# Rmarkdown article template for Rstudio

## 使用方法

### 软件要求

1. **R**：
   - 下载地址：
     https://mirrors.tuna.tsinghua.edu.cn/CRAN/bin/windows/base/old/3.5.3/R-3.5.3-win.exe
   - 下载 `R` ，安装之后设置环境变量如 `C:\Worktools\R\R-4.1.1\bin\x64` ，具体路径
	  根据自己安装位置确定，必须要添加 `R` 安装文件的 `\bin\x64` ，
   - 然后在`cmd` 中运行 `r` ，若不出错则安装成功。
2. **R packages**: 
   - 在 `cmd` 中运行 `R`后再分别运行 `install.packages('knitr')` ，
   `install.packages('rmarkdown')` ，`install.packages('bookdown')` ，
   `install.packages('reticulate')` 四条代码，
   - 运行成功之后再分别运行
   `library(knitr)` ， `library(rmarkdown)` ，`library(bookdown)`，
   `library(reticulate)` ，如果都加载成功说明已安装好。
3. **Rstudio**
4. **`Anaconda`** (运行Python代码必需)：
   - 下载安装 Anaconda，网址：
	  https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-2019.10-Windows-x86_64.exe
   - 安装过程中注意要选择添加到Path中选项.
   - 安装在根目录下面，如 `C:\Anaconda3` 或 `D:\Anaconda3` 等.
5. **`Latex`** (生成pdf和beamer必需)： 
   - 可安装 `TexLive`(安装文件3.3G，安装需要约6G空间)，
   - 下载地址：https://pan.baidu.com/s/13Gisi-BYGn-p-FoWrbAYyg 提取码：v8tr
   - 下载后直接解压，把文件夹 `C:\texlive\2019\bin\win32` 添加到环境变量 


### 在 Rstudio 中编译

2. Rstudio 自动把Rmarkdown 文件中 `yaml header` 中的 `true` 等改成 `yes`， 导致 `pandoc-crossref` 程序出错
3. Rstudio 不能读取 `_output.yml` 文件中的内容
   
## 编译常见错误的原因及解决方法

```diff
-----------------使用以下解决方法，必须先阅读下面的注意(必读)--------------
```

**================ 注意(必读) ================** 

1. **以下解决方法必须先设置好环境变量修改方法一：使用命令行，把项目中文件夹中的
   `SetEnv.exe` 文件放入 `C:\Windows\System32` 文件夹中**
2. 以下解决方可能需要**重启Rstudio**才能发挥作用; 
3. 文件路径必须**改成自己的文件路径**; 

```diff
-----------------使用以下解决方法，必须先阅读上面的注意(必读)--------------

**常见错误**
1. 找不到 `knitr` 等包
2. 找不到 `python` 或其 `package`
3. 出现 `QT` 错误， `python` 图形出不来
4. 不能生成 `pdf` 和 `beamer`
5. `pdf` 文件中中文字符乱码


**常见错误原因及解决方法**

1. 找不到 `knitr` 等包
   - 原因： `R` 中相关包没有安装好
   - 解决方法： `R`中安装相关包，具体见上面软件要求的第3条.
2. 找不到 `python` 或其 `package`
   - 原因： `R`的 `reticulate` 包找不到 `Anaconda`的`python`程序
   - 解决方法： 在 `CMD` 中运行 `setenv -ua  RETICULATE_PYTHON C:\Anaconda3\python.exe`
3. 出现 `QT` 错误， `python` 图形出不来
   - 原因：操作系统中装有其他 `QT platforms`(特别是onedrive软件)，导致` python` 不能
     使用自带的 `QT platform`
   - 解决方法：在 `CMD` 中运行 `setenv -ua QT_QPA_PLATFORM_PLUGIN_PATH C:\Anaconda3\Library\plugins\platforms`
4. 不能生成 `pdf` 和 `beamer`
   - 原因： 没有安装 `latex` 软件或者没有加入环境变量
   - 测试方法： `CMD` 中输入 `xelatex` 没有出现错误则表明 `latex` 设置成功
   - 解决方法： 安装最新版 `Latex` 发行版并加入到 `PATH` 环境变量中，见上面软件要求
     第6步
5. `pdf` 文件中中文字符乱码
   - 原因： 可能字体问题或 `Latex` 不是新版原因
   - 解决方法：安装新版 `Latex`，如上面`TexLive`
	
# RMD-ARTICLE-TEMPLATE介绍
## 项目文件结构

该项目是一个论文模板,其主要文件结构为

```
\---rmd-article-template
    |   beamer-header.tex
    |   Bibfile.bib
    |   rmd-template.Rmd
    |   znufelogo.jpg
    |   _bookdown.yml
    \---style
            beamer-template.tex
            bookdown-pdf-template.tex
            chinese-gb7714-2005-numeric.csl
            default-1.17.0.2.tex
            gbt7714-plain-zuel.bst
            markdown.css
            word-styles-01.docx
            word-styles-02.docx
```

共包含1个子文件夹,分别是`style`和其余6个文档,分别是
`_bookdown.yml`,`bermer-header.tex`,`Bibfile.bib`,`rmd-template.Rmd`,`znufelogo.jpg`。
下面逐一做简单介绍。
1. `style`部分还包括几个用来控制论文生成格式的子文件,如参考文献格式,word文档生成格式等;
2. `_bookdown.yml`是`bookdown`文档中相关字符的说明;
3. `bermer-header.tex`是生成幻灯片时,对作者,邮箱以及logo的设置;
4. `Bibfile.bib`文件放置了用`Jabref`整理的固定格式的参考文献文本文档;
5. `rmd-template.Rmd`是论文正文部分;
6. `znufelogo.jpg`即生成幻灯片时的Logo。

### rmd-template.rmd相关说明

1. rmd-template.rmd文档名称`rmd-template`可自行修改
2. 在rmd-template.rmd中,`title`,`author`,`date`,`institute`冒号后的内容可自行修改。
3. 从`TODO`到`## 使用方法`可删除，使用rmd格式编辑文档内容。
4. 文中其他内容均为格式设计不要随意更改。
5. 文末如下的最后两行不要更改，始终放在文末，通过编辑文件夹中`Bibfile.bib`插入参考文献。
   ```
   # 参考文献
   [//]: # (\bibliography{Bibfile})
   ```

### rmd生成幻灯片beamer内容相关说明

1. 选择`rmd-beamer`生成了5个文件，分别是`rmd-template_beamer.pdf`、`rmd-template_beamer.log`、`rmd-template_beamer.tex`、`rmd-template.py`、`rmd-template.R`,其中`rmd-template_beamer.pdf`是我们所需要的幻灯片内容。
2. 在rmd-template.rmd中,`institute: 中南财经政法大学统计与数学学院`只在幻灯片中显示。`classoption: "aspectratio=1610"`，1610 是幻灯片的长宽比例，有1610,169,43等选择，调整幻灯片长宽。
3. 关于幻灯片中邮箱和右下角图标logo的修改：
   - 修改图标：`znufelogo.jpg`是幻灯片右下角的图标，可更换为其他jpg图片。打开`beamer-header.tex`,将第二行最后`{./znufelogo.jpg}`中的`znufelogo`改为需要替换的jpg图片名称,需替换的jpg图片要放在当前文件夹中。
   - 修改邮箱：打开`beamer-header.tex`,第一行将两个`某某`修改为文章作者名,将`xxxx@zuel.edu.cn`修改为自己的邮箱
   - 打开`_output.yml`,第47行取消注释`in_header: ./beamer-header.tex`。
   - 做出以上修改后，运行`rmd-beamer`,生成的幻灯片中邮箱和图标logo已经修改。
   
### footnote 相关问题
1. markdown 中用 `^[脚注内容]` 来增加脚注
2. 正文中的脚注所有输出格式都支持
3. title 和 author 中的脚注 docx 和 html默认支持，article 和 bookdown 中由于使用
   了 `titling.sty` ，需要 HACK `titling.sty` 才可以支持， beamer 中不能支持，只
   能在 `YAML` 中使用 `thanks` 来支持.

