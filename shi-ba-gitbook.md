---
description: 作者：雪之梦技术
---

# 十八、gitbook

`gitbook` 生成电子书主要有三种方式:

* `gitbook-cli` 命令行操作,简洁高效,适合从事软件开发的相关人员.
* `gitbook-editor` 编辑器操作,可视化编辑,适合无编程经验的文学创作者.
* `gitbook.com` 官网操作,在线编辑实时发布,适合无本地环境且科学上网的体验者.

本文主要讲解第一种 `gitbook-cli` 命令行操作流程,其他两种见另外两篇教程.

### 安装gitbook

#### 环境要求

* `git`（可选）：版本控制系统
* `node.js`（必须）：js 在服务端运行的环境基础，gitbook3.2.3，Windows版node-v12.18.3-win-x64，有BUG，回退到10版本就可以了

> `nodejs` 默认的包安装工具 `npm` 国内访问速度有点慢,安装完毕后建议 `npm install cnpm -g --registry=https://registry.npm.taobao.org` 使用淘宝镜像源代替默认的 `npm` ,详细教程请参考官方 [https://nodejs.org/](https://nodejs.org/en/)

#### `gitbook` 安装

安装 `gitbook-cli` 脚手架工具:

    $ sudo npm install -g gitbook-cli

    # 打印出 `CLI` 和 `GitBook` 版本信息即可,安装版本可能已经大于 `2.3.2`
    gitbook --version
    CLI version: 2.3.2
    GitBook version: 3.2.3

{% hint style="info" %}
`gitbook-cli` 是 `gitbook` 的脚手架工具,帮助我们更方便构建 `gitbook` 应用,当然也可以直接安装 `gitbook` ,只不过那样的话,略显麻烦,不推荐.
{% endhint %}

### `gitbook` 的一些常用命令:

```text
gitbook init     # 初始化目录文件
gitbook help     # 列出gitbook所有的命令
gitbook --help   # 输出gitbook-cli的帮助信息
gitbook build    # 生成静态网页
gitbook serve    # 生成静态网页并运行服务器
gitbook build --gitbook=2.6.7     # 生成时指定gitbook的版本, 本地没有会先下载
gitbook ls                   # 列出本地所有的gitbook版本
gitbook ls-remote            # 列出远程可用的gitbook版本
gitbook fetch 标签/版本号     # 安装对应的gitbook版本
gitbook update               # 更新到gitbook的最新版本
gitbook uninstall 2.6.7      # 卸载对应的gitbook版本
gitbook build --log=debug    # 指定log的级别
gitbook builid --debug       # 输出错误信息
```

### markdown 基本知识

```text
# 标题1
## 标题2

1. 有序列表1 
2. 有序列表2 
3. 有序列表3

- 无序列表1 
* 无序列表2 
+ 无序列表3
----------------------------------------
链接：
[文字](http://bruce-sha.github.io "tip")
[不如][1]
[1]:http://bruce-sha.github.io
自动链接：<http://ibruce.info>

图片：
![图片标题]](图片地址)

---------------------------------------
代码块：
`code`

```
function fun(){
 echo "这是一句非常牛逼的代码";
}
fun();
```

----------------------------------------- 
半方大的空白&ensp;或&#8194;看，飞碟
全方大的空白&emsp;或&#8195;看，飞碟
不断行的空白格&nbsp;或&#160;看，飞碟
&emsp;&emsp;段落从此开始。
 
<font face="黑体">我是黑体字</font>
<font face="微软雅黑">我是微软雅黑</font>
<font face="STCAIYUN">我是华文彩云</font>
<font color=#0099ff size=12 face="黑体">黑体</font>
<font color=#00ffff size=3>null</font>
<font color=gray size=5>gray</font>
```

### 新建书籍示例

执行命令 `gitbook init testbook` ,则会自动生成一个最基本的书籍骨架：

```text
$ gitbook init testbook

info: init book at testbook
info: detect structure from SUMMARY (if it exists)
info: create SUMMARY.md
info: create README.md
info: initialization is finished

Done, without error
```

进入 testbook 目录，可以看到只有两个文件：

```text
$ cd testbook/
$ ls
README.md  SUMMARY.md
```

* SUMMARY.md 是书籍的目录和排版，目前文件为空，里面只有一行注释：`# Summary`
* README.md 是书籍的介绍信息，目前只有一个标题：`# Introduction`

 在 testbook 目录下运行命令 `gitbook serve`启动服务，提示如下，说明运行成功，浏览器输入： `http://localhost:4000`即可打开书籍

```text
...
Starting server ...
Serving book on http://localhost:4000
```

一个基本的 GitBook 电子书结构通常如下：

```text
.
├── _book
├── README.md
├── SUMMARY.md
├── book.json
├── GLOSSARY.md
├── LANGS.md
├── chapter-1/
│     ├── README.md
│     └── something.md
└── chapter-2/
       ├── README.md
       └── something.md
```

* `_book` 是默认的输出目录， 执行 `gitbook build` 或 `gitbook serve` **自动生成**的 **静态网站**
* `README.md`电子书的前言或简介 \(required\)，相当于网站首页，是**必须**的
* `SUMMARY.md` 电子书目录 \(optional\)，初始化默认创建的重要文件，是**必须**的
* `book.json` 配置数据 \(optional\)，用于个性化调整，如定义电子书的标题,封面,作者等信息.虽然是手动创建但一般是**必选**的.
* `GLOSSARY.md`词汇/注释术语列表 \(optional\)，手动创建但是**可选的**
* `LANGS.md` 是默认的语言文件,用于国际化版本翻译,和 `GLOSSARY.md` 一样是手动创建但是**可选**的.

#### `book.json` 配置文件\[可选\]

```text
"title": "雪之梦技术驿站"     //书籍的标题
"author": "liangpingguo"   //书籍的作者
"description": 本书主要分享个人的学习经验,一家之言,仅供参考."    //书籍的简要描述
"isbn": "978-0-13-601970-1"     //书籍的国际标准书号
"language": "zh-hans"    //语言
"direction" : "ltr"    //阅读顺序,从右到左(rtl)或从左到右(ltr),默认值取决于语言值
"gitbook": "3.2.3"    //指定 gitbook 版本,支持SemVer规范,接受类似于 >=3.2.3 的条件.

```

> 选填,请参考 [ISBN Search](https://isbnsearch.org/)

**language 语言**

> 支持语言项: 默认英语\(`en`\),设置成简体中文\(`zh-hans`\)

```text
en, ar, bn, cs, de, en, es, fa, fi, fr, he, it, ja, ko, no, pl, pt, ro, ru, sv, uk, vi, zh-hans, zh-tw
```

示例:

```text
"language": "zh-hans"
```

**root 根目录**

> 指定存放 `gitbook` 文件\(除了`book.json`文件本身\)的根目录

示例:

```text
"root": "."
```

**links 侧边栏链接**

> 左侧导航栏添加链接,支持外链

示例;

```text
"links": {
    "sidebar": {
        "我的网站": "https://snowdreams1006.cn/"
    }
}
```

**styles 自定义样式**

> 自定义全局样式

示例:

```text
"styles": {
    "website": "styles/website.css",
    "ebook": "styles/ebook.css",
    "pdf": "styles/pdf.css",
    "mobi": "styles/mobi.css",
    "epub": "styles/epub.css"
}
```

**plugins 插件**

> 配置额外的插件列表,添加新插件项后需要运行 `gitbook install` 安装到当前项目.

`gitbook` 默认自带5个插件,分别是:

* `highlight` 语法高亮插件
* `search` 搜索插件
* `sharing` 分享插件
* `font-settings` 字体设置插件
* `livereload` 热加载插件

> 如需获取更多插件请访问[官网插件市场](https://plugins.gitbook.com/)

示例:

```text
"plugins": [
    "github",
    "pageview-count",
    "mermaid-gb3",
    "-lunr", 
    "-search", 
    "search-plus",
    "splitter",
    "-sharing", 
    "sharing-plus",
    "expandable-chapters-small",
    "anchor-navigation-ex",
    "edit-link",
    "copy-code-button",
    "chart",
    "favicon-plus",
    "donate"
]
复制代码
```

**pluginsConfig 插件配置**

> 安装插件的相应配置项,具体有哪些配置项是由插件本身提供的,应访问插件官网进行查询.

```text
"pluginsConfig": {
    "github": {
      "url": "https://github.com/snowdreams1006/snowdreams1006.github.io"
    },
    "sharing": {
       "douban": true,
       "facebook": false,
       "google": false,
       "hatenaBookmark": false,
       "instapaper": false,
       "line": false,
       "linkedin": false,
       "messenger": false,
       "pocket": false,
       "qq": true,
       "qzone": true,
       "stumbleupon": false,
       "twitter": false,
       "viber": false,
       "vk": false,
       "weibo": true,
       "whatsapp": false,
       "all": [
           "facebook", "google", "twitter",
           "weibo", "instapaper", "linkedin",
           "pocket", "stumbleupon"
       ]
   },
   "edit-link": {
      "base": "https://github.com/snowdreams1006/snowdreams1006.github.io/blob/master",
      "label": "编辑本页"
    },
    "chart": {
      "type": "c3"
    },
    "favicon": "/images/favicon.ico",
    "appleTouchIconPrecomposed152": "/images/apple-touch-icon-precomposed-152.png",
    "output": "_book",
    "donate": {
      "wechat": "/images/wechat.jpg",
      "alipay": "/images/alipay.jpg",
      "title": "赏",
      "button": "捐赠",
      "alipayText": "支付宝",
      "wechatText": "微信"
    }
}
复制代码
```

**pdf 配置**

> 定制 `pdf` 输出格式,可能需要安装 `ebook-convert` 等相关插件

| 配置项 | 描述 |
| :--- | :--- |
| `pdf.pageNumbers` | 添加页码\(默认值是 `true` \) |
| `pdf.fontSize` | 字体大小\(默认值是 `12` \) |
| `pdf.fontFamily` | 字体集\(默认值是 `Arial` \) |
| `pdf.paperSize` | 页面尺寸\(默认值是 `a4` \),支持`a0`,`a1`,`a2`,`a3`,`a4`,`a5`,`a6`,`b0`,`b1`,`b2`,`b3`,`b4`,`b5`,`b6`,`legal`,`letter` |
| `pdf.margin.top` | 上边界\(默认值是 `56` \) |
| `pdf.margin.bottom` | 下边界\(默认值是 `56` \) |
| `pdf.margin.left` | 左边界\(默认值是 `62` \) |
| `pdf.margin.right` | 右边界\(默认值是 `62` \) |

> 电子书封面照片 `cover.jpg` 和 `cover_small.jpg`,后续会详细说明.

#### `GLOSSARY.md` 词汇表文件\[可选\]

词汇表文件,用于全书的专业词汇解释说明,比如鼠标悬停在专业词汇上会有相应提示.

> 语法格式: `##` + + `专业词汇`

学习 `gitbook` 前最好先学习下markdown和git,你知道他们的用途吗?

示例:

```text
## markdown
简洁优雅的排版语言,简化版的 `HTML`,加强版的 `TXT`,详情请参考 [https://snowdreams1006.github.io/markdown/](https://snowdreams1006.github.io/markdown/)

## git
分布式版本控制系统,详情请参考 [https://snowdreams1006.github.io/git/](https://snowdreams1006.github.io/git/)
复制代码
```

#### `LANGS.md` 语言文件\[可选\]

支持国际化编写图书,一种语言一个单独子目录,同样地,将语言文件放到根目录下.

示例:

```text
* [English](en/)
* [French](fr/)
* [Español](es/)
```

### Grunt安装

> 注：只有需要将内容发布到github pages时才需要grunt

通过下列命令安装 grunt 和 grunt-cli

```text
npm install -g grunt grunt-cli
```

安装完成之后，执行 `grunt --version` 命令可以看到当前安装的版本：

```text
$ grunt --version
grunt-cli v1.2.0
```

