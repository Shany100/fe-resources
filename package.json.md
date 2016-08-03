# package.json
## npm 的 package.json 的处理细节。

#### 描述
这个文档是关于在你的 package.json 文件里，你需要了解什么是必须。它必须是 JSON 格式的，不仅仅是 JavaScript 对象。

在这个文档里所描述的大量特性被在 npm-config 里的设置所影响。

#### name
在 package.json 中最重要的字段就是 name 和 version。那些实际需要的，如果没有它们可能你的包安装不了。name 和 version 一起组成一个唯一标识。如果改动了包的内容应该同时更改版本号。

一些规则：
 - name 的值必须少于 214 个字符。这个包含作用域的名称。
 - name 的值不能以```.```和```_```开头。
 - 不能包含大写的字母。
 - 名称会是URL、命令行、文件夹命名尾部的一部分，因此名称不能包含不安全的 URL 字符。


一些提示：
 - 不能与 Node 核心包同名。
 - 不要把"js"和"node"放人名称里。一旦用了 package.json 就默认为 js 相关的文件或项目了，可以通过声明 "engines" 字段声明项目使用的引擎。
 - 名称可能作为```require()```的参数使用，所以尽量简短、语义化。
 - 为避免重名，可以在 npm 官网搜索检测一下。

名称可以有命名空间，使用范围，如 ```@myorg/mypackage```。

#### version
在 package.json 中最重要的字段就是 name 和 version。那些实际需要的，如果没有它们可能你的包安装不了。name 和 version 一起组成一个唯一标识。如果改动了包的内容应该同时更改版本号。

version 的值必须可以被[node-semver](https://github.com/npm/node-semver)所解析。

#### description
它的值是一个字符串，填入后。更容易被用户发现，还有通过 ``` $ npm search ``` 列出来。

#### keywords
它的值是一个字符串数组，填入后。更容易被用户发现，还有通过 ``` $ npm search ``` 列出来。

#### homepage
项目的主页地址 (url)。

#### bugs
这个地址是为了对项目问题的跟踪，或者是电子邮箱方便收集报告。比如：
```
{
  "url": "https://github.com/owner/project/issues",
  "email": "project@hostname.com"
}
```
可以设置一个或两个都存在。假如 url 提供了，可以使用 ``` npm bugs ```命令查看问题列表。

#### license
通过设置这个属性让用户知道什么情况下允许使用。
如：```{ "license" : "BSD-3-Clause" }```

#### people fields: author, contributors

#### files
这个字段描述的是项目中包含的文件列表。可以编写文件 ```.npmignore``` 作用如同``` .gitignore ```。部分文件总是被包含的，不会被设置所影响：
 - package.json
 - README
 - CHANGELOG
 - LICENSE / LICENCE


反过来，有些文件总是被忽略的：
 - .git
 - CVS
 - .svn
 - .hg
 - .lock-wscript
 - .wafpickle-N
 - *.swp
 - .DS_Store
 - ._*
 - npm-debug.log

#### main
main 是一个模块的ID，程序的主入口。比如，模块的名称是 foo，用户安装它后，程序调用 ```require('foo')``` ，然后 main 模块暴露的对象将被返回。关联这模块目录的根目录。对于大多数模块来说，然后有一个主要脚本。

#### bin
大部分包都有一个或多个可以执行文件。
