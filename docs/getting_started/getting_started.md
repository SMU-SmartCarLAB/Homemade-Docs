# Getting started
本教程将涵盖如何开始使用文档托管服务并上传自己的文档。  
诚挚的感谢每一位为我们的知识库添砖加瓦的成员。  
## 环境配置  
本文档托管服务基于MkDocs进行Markdown至HTML文件的编译，使用ReadTheDocs服务完成在线自动编译，要开始撰写您的文档，请先在本地搭建MkDocs服务。  
环境要求：`Python >= 3.8` `pip >= 20.0`   

### 安装本地MkDocs服务  
```text
$ pip install mkdocs
```  
### 克隆GitHub仓库
```text
$ git clone https://github.com/SMU-SmartCarLAB/Homemade-Docs.git
```  
### 验证本地MkDocs服务安装成功
进入克隆的GitHub仓库文件夹根目录，其中应该包含`mkdocs.yml`文件，在当前文件夹启动MkDocs服务。  
```text
$ mkdocs serve
```
如服务安装正确，应该产生如下输出   
```text
INFO    -  Building documentation...
INFO    -  Cleaning site directory
INFO    -  Documentation built in 0.22 seconds
INFO    -  [15:50:43] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO    -  [15:50:43] Serving on http://127.0.0.1:8000/
```
前往[http://127.0.0.1:8000/](http://127.0.0.1:8000/)查看编译完成的HTML网页，至此本地MkDocs服务安装完成，在您将创建的文档上传至Github仓库之前，请先运行本地MkDocs服务并验证文档编写正确。只要本地端口上的MkDocs服务仍在运行，您对文档的修改将实时反映在本地端口上的网页中，这使您可以在编写文档的同时实时检查文档是否像期望中的那样正确展示。    

要结束本地端口上的MkDocs服务，请`Ctrl+C`
## 熟悉MkDocs文件结构
### 工程目录结构
一个MkDocs工程包含以下目录结构：
```text
mkdocs.yml                         --配置文件，无需修改
docs/                              --docs文件夹，存放所有文件
    index.md                       --主页文件
    chapter1/                      --章节文件夹
              how_to_build_a_spaceship.md    --章节中的markdown文档
              fundamentals_of_rocket_science.md
              ....
              img/                              --图片文件夹，存放需要在文档中展示的图片
                  grapes_in_the_microwave.jpg
                  ...
    ...
```
您撰写的文档应该放置于`/docs`文件夹中，**请为撰写的章节创建一个相应的文件夹**，并将撰写的Markdown文件放置在文件夹中。是否为章节中的二级章节创建文件夹无强制规定，但是建议为每个二级章节创建文件夹以方便整理。

!!! warning
    **不要随意修改或删除不是自己创建的文档**，请互相尊重他人的劳动成果。  

创建文档和文件夹时，**请注意文档名称仅支持英文字符**，文档名称应当清晰的表达文档包含的内容主题且不宜过长，**禁止使用拼音**，单词之间使用下划线`_`进行分隔。

如需在文档中插入图片，请在存储Markdown文件的文件夹路径下创建一个`img`文件夹放置需要插入的图片，由于本仓库托管在GitHub并且我们买不起付费账户，为了减小仓库体积，请使用JPG格式的图片并尽量控制图片大小小于`700KB`。 

!!! note
    [Python-Markdown](https://python-markdown.github.io/)对图片的索引使用相对路径完成，即实际的图片路径应该为`/markdown文件路径`+`/插入图片时指定的路径`。如在插入图片时指定路径为`img/pic1.jpg`，而Markdown文件存储的绝对路径为`docs/chapter1/topic1`，则图片的绝对路径应为`docs/chapter1/topic1/img/pic1.jpg`

### 设置章节导航栏
在工程根目录下找到`mkdocs.yml`文件，其中包含章节导航栏的配置：  

!!! warning
    禁止修改`mkdocs.yml`中除了`nav:`以外的部分，修改时也不要破坏不是由自己创建并已经存在的导航结构。
```yml
nav:                 --导航栏配置
  - Home: index.md   --主页
  - "使用指南":       --一级章节标题
      - getting_started/getting_started.md   --页面文件
  - Chapter1:        --一级章节标题
      - Topic1:      --二级章节标题
        - chapter1/topic1/page1.md   --页面文件
        - chapter1/topic1/page2.md
```
其中，`nav:`标识导航栏配置起始，`-Home: index.md`为主页，其后的部分为用户可配置的导航目录，章节最多包含两级标题。  

!!! note
    一个章节既可以使用二级标题结构也可以使用一级标题结构，但是仅能在最低一级的标题下包含页面的`Markdown`文件。
正确的操作：

```text
- Chapter1:                         --一级章节标题
    - Topic1:                       --二级章节标题
        - chapter1/topic1/page1.md  --页面文件
        - chapter1/topic1/page2.md
```  

同样也是正确的操作：

```text
- Chapter1:                         --一级章节标题
    - chapter1/page1.md             --页面文件
    - chapter1/page2.md
```

错误的操作：

```text
- Chapter1:                         --一级章节标题
    - chapter1/page1.md             --页面文件
    - Topic1:                       --二级章节标题
        - chapter1/topic1/page2.md  --页面文件
```

### 编写文档文件
MkDocs接受使用标准Markdown语法编写的文档，文件后缀名为`.md`,关于Markdown语法的更多内容，可以参考[Markdown教程](https://markdown.com.cn/)。   

MkDocs会按照Markdown文件中的标题层级为每一个Markdown文件生成导航栏，共支持三级标题结构，一级标题将被作为页面的启始标题，二三级标题构成包含在一级标题下的下拉列表，点击相应的标题即可跳转到对应的文档位置，三级以下的标题将不会展示在MkDocs导航栏中，但其在文档中的展示样式依旧遵循Markdown标题的渲染规则。另外，在`mkdocs.yml`中设定的章节标题将作为大标题生成在所有此章节的文件之上。

在文档中插入图片的操作与常规Markdown文档相同，请使用感叹号 (!), 然后在方括号增加替代文本，图片链接放在圆括号里，括号里的链接后可以增加一个可选的图片标题文本。  
like this: `![图片alt](图片链接 "图片title")`  特定于本工程的结构下，图片链接应该为`img/图片名字.jpg`   

如这段文本将产生如下的图片插入效果
```markdown
![grapes in the microwave](img/grapes_in_the_microwave.jpg "不要把葡萄放进微波炉")
```
![grapes in the microwave](img/grapes_in_the_microwave.jpg "不要把葡萄放进微波炉")
## 部署您的文档
受益于本工程使用了[Read The Docs](https://about.readthedocs.com/) 的在线自动编译服务，只需要将修改完成的仓库push至GitHub就会触发自动编译操作，编译过程耗时1-5分钟不等，编译完成的HTML网页可直接在[本网站](https://docs.smuscl.org/zh-cn/latest/) 查看。  

<del>是的这个服务是免费的所以会有广告您要是不喜欢可以赞助我们买付费的服务。</del>  

## 一些技巧
由于MkDocs使用[Python-Markdown](https://python-markdown.github.io/)完成HTML文件的构建，其对于不属于[Markdown syntax rules](https://daringfireball.net/projects/markdown/syntax)中的方式未提供原生支持，例如大部分的[扩展语法](https://markdown.com.cn/extended-syntax/)。当然MkDocs默认内置了一些Python-Markdown插件来支持现代化的Markdown扩展语法，以下是测试已知的可用[扩展语法](https://markdown.com.cn/extended-syntax/)和[扩展语法](https://markdown.com.cn/extended-syntax/)的替代方式。  
### 可用的扩展语法
#### 围栏代码块
在开头和结尾行使用三个`` ``` ``来构成围栏代码块，并且可以在`` ``` ``后添加代码的类型如`C++`来触发高亮显示。
````text
```C++
#include <iostream>
using namespace std;
int main()
{
    cout << "Hello, world!" << endl;
    return 0;
}
```
````
这将输出为
```C++
#include <iostream>
using namespace std;
int main()
{
    cout << "Hello, world!" << endl;
    return 0;
}
```
如需要在围栏代码块中展示`` ``` ``符号，使用四个反引号`` ```` ``替代三个反引号。
#### 表格
要添加表格，请使用三个或多个连字符`---`创建每列的标题，并使用管道`|`分隔每列。您可以选择在表的任一端添加管道。
```markdown
| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |
```
这将输出为  

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |  

#### Admonitions
要添加警告/信息(Admonitions)块，使用三个感叹号`!!!`并在其后跟随需要显示的标题，部分标题拥有特定的渲染外观，块内容启始于下一行，并由四个空格构成每一行块内容的开头。
```
!!! note
    试试看把两个葡萄放进微波炉
```
这将输出为  

!!! note
    试试看把两个葡萄放进微波炉
已知可以触发特殊渲染外观的标题词：  

!!! warning
    不要把两个葡萄放进微波炉

!!! tip
    每次最多把一个葡萄放进微波炉

!!! danger
    把两个葡萄放进微波炉会发生意想不到的事情

当然，也可以使用任意文字作为标题

!!! 你真的要把两个葡萄放进微波炉吗
    哈哈 

### 使用HTML样式替代
Markdown支持使用原生HTML方法直接进行样式替代，如果想要实现不受[Markdown syntax rules](https://daringfireball.net/projects/markdown/syntax)支持的样式方法，可以考虑直接使用HTML样式。  
例如使用删除线:
```html
<del>嘤嘤嘤我被删除了</del>
```
这将展示为  
<del>嘤嘤嘤我被删除了</del>

## 良好的工作习惯
所有成员在开始撰写自己的文档时，首先应该使用`git pull`操作拉取远程分支中存在的更改，并签出到一个新的分支进行编写，编写完成并成功推送至远程分支后再进行合并操作，这样可以避免多人同时在主分支编写而造成推送时产生变更记录无法吻合的报错。虽然本工程不是传统意义上的代码工程，也几乎不会出现多人同时修改一个文档的操作，但还是希望大家养成良好的工作习惯，避免产生不必要的问题。

#### Happy Writing and Sharing.



