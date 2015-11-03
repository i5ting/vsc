# extra practice

## 使用oh-my-zsh

- 官网 http://ohmyz.sh/
- 代码 https://github.com/robbyrussell/oh-my-zsh

安装步骤

- 先安装zsh
- 安装oh-my-zsh

以后环境变量在~/.zshrc里

## alias

俗称别名，在git里面我们最常用的命令是查看状态，可以又太长

于是

```
vi ~/.zshrc
```

增加如下别名定义

```
alias gs='git status'
```

source使环境变量生效（如果不想重启电脑的话）

```
source ~/.zshrc
```
如果不理解环境变量，自己去闭门思过去

## 杀死所有nodejs相关进程

```
ps -ef|grep node|awk '{print $2}'|xargs kill -9
```

- ps -ef查看进程
- grep node是过滤进程里的和node相关的所有进程
- awk '{print $2}' 取出进程号
- xargs kill -9 杀掉该进程

`|`是pipe，即管道的意思：上一个的输出，是下一个的输入

如此理解变掌握了shell的精髓

## 命令行查找代码

ack是一个perl脚本，是grep的一个可选替换品。其可以对匹配字符有高亮显示。是为程序员专门设计的，默认递归搜索，省提供多种文件类型供选。

http://beyondgrep.com/install/


Ubuntu
    
- Package "ack-grep"

Mac

- brew install ack

mac下面直接用，linux记得自己alias一下

检索文本内的key是非常高效的

```
➜  vsc-doc git:(master) ✗ ack i5ting
extra.md
72:https://github.com/i5ting/awesome-mac-practice2/blob/master/app/Dash.zip?raw=true

preview/index.html
434:<li><a href="http://i5ting.github.io/nodejs-video/node-inspector.mov">node-inspector视频</a></li>
435:<li><a href="http://i5ting.github.io/nodejs-video/node-debug.mov">node-debug视频</a></li>
525:<p>这其实和<a href="http://i5ting.github.io/How-to-write-jQuery-plugin/build/jquery.plugin.html#10501">jquery插件里的配置项</a>原理是类似的</p>
1307:<p>详见 http://i5ting.github.io/vsc-course/ </p>

preview/README.html
434:<li><a href="http://i5ting.github.io/nodejs-video/node-inspector.mov">node-inspector视频</a></li>
435:<li><a href="http://i5ting.github.io/nodejs-video/node-debug.mov">node-debug视频</a></li>
525:<p>这其实和<a href="http://i5ting.github.io/How-to-write-jQuery-plugin/build/jquery.plugin.html#10501">jquery插件里的配置项</a>原理是类似的</p>
1307:<p>详见 http://i5ting.github.io/vsc-course/ </p>

preview/toc/js/ztree_toc.js
2:* https://github.com/i5ting/jQuery.zTree_Toc.js

README.md
313:- [node-inspector视频](http://i5ting.github.io/nodejs-video/node-inspector.mov)
314:- [node-debug视频](http://i5ting.github.io/nodejs-video/node-debug.mov)
427:这其实和[jquery插件里的配置项](http://i5ting.github.io/How-to-write-jQuery-plugin/build/jquery.plugin.html#10501)原理是类似的
1266:详见 http://i5ting.github.io/vsc-course/ 
```

其实go写的[fzf](https://github.com/junegunn/fzf)也很棒

##  查询文档神器

- http://zealdocs.org/ (推荐，离线下载)

有很多doc在[dash](https://github.com/i5ting/awesome-mac-practice2/blob/master/app/Dash.zip?raw=true
)（mac）里默认是没有的；

see here ： http://kapeli.com/docset_links

如果是下载到本地的docset，放到zealdocs目录下面，需要重启zeal


- linux 叫zeal
- mac 叫dash

都是基于docset的神器

## 目录切换神器

autojump是一个命令行工具，它允许你可以直接跳转到你喜爱的目录，而不用管你现在身在何处。

https://github.com/wting/autojump

Linux

    sudo apt-get install autojump
    
Mac os

    brew install autojump
    
需要修改~/.zshrc里的plugin,修改为

    plugins=(git autojump)

然后

    source ~/.zshrc
    
至此，已经完成了安装。

此后cd到任意目录，以后就可以使用j这个直达到某个目录了，下面是示例：

    ➜  nodejs-newbie git:(master) ✗ cd ~/workspace/github/nodejs-newbie
    ➜  nodejs-newbie git:(master) ✗ cd ~
    ➜  ~  j nodejs-n
    /Users/sang/workspace/github/nodejs-newbie
    ➜  nodejs-newbie git:(master) ✗ 
  
如果想玩的更high，可以参见https://github.com/clvv/fasd

## 根据端口号查看进程

lsof是系统管理/安全的工具，列出打开文件（lists openfiles）

```
$ lsof -i:3005
COMMAND   PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
node    30438 sang   26u  IPv6 0xd9428cd06d17f6af      0t0  TCP *:geniuslm (LISTEN
```

于是衍生一下，根据端口杀进程，比如express默认是3000端口，难免有时有僵尸进程，如果直接根据端口杀死，是不是很爽？

```
lsof -i:3005|xargs killall
```

再衍生一下，能不能封装成一个nodejs模块，端口号作为参数，完成上述功能呢？

于是有了kp

kp is a tool for kill process by server port

    [sudo]npm install -g kp
    kp 3002

https://github.com/i5ting/kp

## mongodb客户端

推荐 www.robomongo.org 

- 支持win
- 支持linux
- 支持mac（mac10.10下中文乱码，需要robomongo v0.8.5+）

这个是最好用的，但是每次启动都比较麻烦

- mac下面使用quicksilver或spotlit
- linux使用alias rogo='robomongo'

## 使用node-inspector调试Node代码

看我写的三法三例调试教程

https://cnodejs.org/topic/5463f6e872f405c829029f7e

## 使用mongoose-cli数据库建模

随时随地，测试model，融合bluebird等promise库，让业务处理更简单

https://cnodejs.org/topic/55c44f0db98f51142b367b54

## mongo here 

当前目录启动mongodb

在新建目录执行

    mh
    
它会创建tmp目录

全局启动mongodb

    mhg
    
它会创建~/mongo/目录，当前用户下起mongo服务，即用户下全局共享

https://github.com/i5ting/mongo-here

核心原理很简单,写个shell脚本，执行命令mh的时候执行它就好了

```
#! /bin/bash

mkdir -p tmp/db
mkdir -p tmp/pids
mkdir -p tmp/logs


# remove lock file
[ -f tmp/db/mongod.lock ] && rm -rf tmp/db/mongod.lock

touch tmp/pids/mongodb.pid

# mongod --bind_ip 192.168.1.100 --port 27017 --dbpath tmp/db --logpath tmp/logs/mongodb.log --pidfilepath tmp/pids/mongodb.pid
nohup mongod --bind_ip 127.0.0.1 --port 27017 --dbpath tmp/db --logpath tmp/logs/mongodb.log --pidfilepath tmp/pids/mongodb.pid >mongod.log 2>&1 &
```
此处是在当前目录下面建立tmp目录，所以保证了权限等问题

mhg其实更简单，就是在用户主目录`~`下建


## json editor 

    [sudo] npm install -g je
    je

详见https://github.com/i5ting/je

## nodejs里的csv处理

    [sudo] npm install -g j2csv
    json2csv
    
详见https://github.com/i5ting/json2csv

上面给出的方案适合3000条以内的数据，受限于浏览器

更大量的数据，需要

    [sudo] npm install -g ej
    ej input.json output.csv
    
https://github.com/i5ting/ej

很多时候，实现导入导出，见

https://github.com/i5ting/i-csv

## upload-cli

a node cli tools for uploads ui

https://github.com/i5ting/upload-cli

- 目前已经支持通过命令行`uci`上传，可指定host

## 编写markdown文档

- 生成markdown模块
- markdown编译成html
- 支持table of content
- 能够push到git pages上

为了markdown toc，我写了https://github.com/i5ting/i5ting_ztree_toc

然后写了一个nodejs模块https://github.com/i5ting/tocmd.npm，用于编译markdown，按照toc模板编译

当然，每次发布到gitpages，我很不爽，于是使用gulp里的`gulp-gh-pages`直接自动化

最后我想更懒点

于是就有了https://github.com/i5ting/docto

一条命令全部搞定

# 如何编写nodejs命令行模块？

上面给出的很多都是nodejs写的小工具模块，nodejs和npm的种种好处，使得nodejs开发命令行模块异常简单


具体做法

## 创建git repo

github上创建即可

## git clone到本地

	git clone git@github.com:i5ting/node-cli-demo.git
	
##  切换到项目目录

	cd node-cli-demo

## 初始化npm

执行

```
npm init
```

一直回车，除非你真的有东西想改动，具体如下

```
➜  node-cli-demo git:(master) npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sane defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (node-cli-demo) 
version: (1.0.0) 
description: 
entry point: (index.js) 
test command: 
git repository: (https://github.com/i5ting/node-cli-demo.git) 
keywords: 
author: 
license: (ISC) 
About to write to /Users/sang/workspace/github/node-cli-demo/package.json:

{
  "name": "node-cli-demo",
  "version": "1.0.0",
  "description": "node-cli-demo =============",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/i5ting/node-cli-demo.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/i5ting/node-cli-demo/issues"
  },
  "homepage": "https://github.com/i5ting/node-cli-demo"
}


Is this ok? (yes) 
➜  node-cli-demo git:(master) ✗ 
```

## 创建文件

	mkdir bin
	mkdir test

	touch bin/node-cli-demo.js
	touch test/node-cli-demo.js

	touch index.js
	touch gulpfile.js

## 修改package.json

### 命令配置（至关重要）

```
  "preferGlobal": "true",
  "bin": {
    "badge": "bin/badge.js"
  },
```

此处是关键

`preferGlobal`确定你的这个命令是不是全局的，一定要设置为true，不然不放到path里，不能全局用的。


`bin`是配置你的cli名称和具体哪个文件来执行这个的
	
### scripts

```
  "scripts": {
    "start": "npm publish .",
    "test": " node bin/badge.js -t js -n q "
  },
```

这里定义了2个命令

- `npm start`

这里我用它发布当前npm到npmjs.org上

- `npm test`

这里我用它作为测试代码，避免每次都重复输入

## 发布

发布之前要注册npmjs账户的

  npm login(只需要一次，以后就不用了)
	npm start

## 更多

推荐几个解析命令行args的库

- commander是tj写的，一个不错的库
- yargs也不错，更强大，简洁
- ccli是我写的，封装了yargs和基本常用的库	


# 如何快速阅读源码？

## 学习5阶段

- getting start 入门
- guide 指南
- doc 查api
- 阅读源码
- 向开源贡献代码

## 你该阅读源码？

上面已经说了，第四个阶段才是读源码

原因是，必须熟练才有用，不然读了也白扯

- 熟练使用该模块
- 熟练掌握npm
- 熟练掌握nodejs语法

有了这个前提你就可以阅读了。

当然事情也不能绝对，没这些，你也可以看，从中找出有用的写法或者学习代码规范也是好的。

## 看目录结构（express框架）

```
➜  express git:(master) ✗ tree . -L 2
.
├── History.md
├── LICENSE
├── Readme.md
├── index.js
├── lib
│   ├── application.js
│   ├── express.js
│   ├── middleware
│   ├── request.js
│   ├── response.js
│   ├── router
│   ├── utils.js
│   └── view.js
├── node_modules
│   ├── accepts
│   ├── array-flatten
│   ├── content-disposition
│   ├── content-type
│   ├── cookie
│   ├── cookie-signature
│   ├── debug
│   ├── depd
│   ├── escape-html
│   ├── etag
│   ├── finalhandler
│   ├── fresh
│   ├── merge-descriptors
│   ├── methods
│   ├── on-finished
│   ├── parseurl
│   ├── path-to-regexp
│   ├── proxy-addr
│   ├── qs
│   ├── range-parser
│   ├── send
│   ├── serve-static
│   ├── type-is
│   ├── utils-merge
│   └── vary
└── package.json

29 directories, 11 files
```

### package.json

这是一个npm模块

- dependencies
- devDependencies
- scripts
- bin
- main
- repository
- license
- homepage

体会细节的差异

### node_modules

放的是当前模块依赖的其他模块

### index.js

npm有一个约定，如果你的项目主文件是index.js可以不在package.json里写明，如果是其他文件就必须写清楚

比如shelljs里的

```
"main": "./shell.js",
```

好了，我们继续看express的package.json，他没有定义main文件，那我们就找index.js

程序入口

```
/*!
 * express
 * Copyright(c) 2009-2013 TJ Holowaychuk
 * Copyright(c) 2013 Roman Shtylman
 * Copyright(c) 2014-2015 Douglas Christopher Wilson
 * MIT Licensed
 */

'use strict';

module.exports = require('./lib/express');

```

### lib

从index.js可知，里面的功能都写在了lib里，也就是说，这里才是最重要的战场

### 其他

```
├── Readme.md 最重要的文档
├── History.md 一般是更新历史
├── LICENSE 授权协议
```

类似的文件写的都比较清楚，需要的时候再看不急

## 建立大局观

大局观有2种

- 目录结构，npm，约定等，属于常识类
- 代码大局观

先大致看一遍，花个个把小时，一定要都看了，不求看懂，但求不放过每一个文件

这就好比买书一样，如果头一周么有看完，这辈子这边书看完的可能性就很渺小了

### 模块阅读

- 根据头3步骤（入门，指南，文档）的理解，大致可以猜出一些，比如（req，res，router，view，middleware）
- 根据文件结构，index指向lib/express,那这就是入口，看看里面组装关系，又明白一层
- 每个文件去读，里面多少有点熟悉的东西

### 源码阅读

package.json里的files

.npmignore

- 先看test、benchmark、examples
- 其他步骤同上

## 带着问题去探索

比如我想获得访问此网页人的ip

## 扒出来的都是自己的

从代码里学，才是最常久的，开源的东西已经足够多了

每天打开github，看一下

https://github.com/trending

最近比较火的项目都有了，挑喜欢的扒一扒，肯定是有你不会的

## 贡献源码，回馈社区

开源是一种精神，从中受益，也要记得反馈社区，这是做程序员最基本的道德。


# 作业

## express调试

## 快捷键练习

## extra练习

## 编写一个node命令行模块

## 阅读一个github上开源项目，写源码分析笔记

下周一前提交给我，sang@aircos.com，我会review，过时不候