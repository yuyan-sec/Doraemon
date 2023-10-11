## Doraemon-渗透辅助小工具

### 前言

1. 在渗透测试或挖 SRC 的时候每次都需要在笔记中复制一些 Payload 或 Webshell 内容觉得太麻烦了，所以打算 **抄一个** Burpsuite 插件，直接在 Burpsuite 点一点操作就简单多了。
2. 在复现一些Http 请求的漏洞，每次都需要在笔记复制exp或写个简单的 python 脚本觉得太麻烦了，如果在 Burpsuite 中直接修改请求包就简单多了。
3. 每次都需要到其他目录打开一些工具，直接在BurpSuite 打开其他工具进行目录扫描等操作就简单多了



### 使用

下载压缩包，修改DAM目录下的目录或文件

- Exp 目录（不能修改目录名）是漏洞相关的，会**修改整个数据包**

- Payload 目录（不能修改目录名），把 **Payload 插入到数据包中**

- `{{Host}}`  或 `{{Hostname}}` 自动获取相关的 Host
- `{{Cookie}}`  获取Cookie



目录架构：可以在Exp或Payload目录下随意新建目录或文件。

```
├─Exp
│  ├─OA漏洞
│  │  ├─OA
│  │  │   漏洞1.txt
│  │  ├─OA2
│  │  │   漏洞2.txt
└─Payload
    └─Webshell
        ├─哥斯拉
        │      jsp.txt
        ├─冰蝎
        │      jsp.txt
```

漏洞1：把漏洞的数据包保存为文件，修改相关的 Host ,Cookie。

```http
GET / HTTP/1.1
Host: {{Host}}
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36 Edg/89.0.774.68
Cookie: {{Cookie}}
Connection: close


```





![](./images/1.png)



#### tools.yaml

可以直接在GUI直接新增和删除，也可以手动添加

```
Tools:
- [test, '{request}']
- [test2, '{url}']
- [test3, '{host}']
- [test4, '{domain}']
- [test5, '{target}']

```

**配置**

https://www.baidu.com/index.php

- {request} 表示使用请求包
- {url} : https://www.baidu.com/index.php
- {host} : www.baidu.com
- {domain} :  baidu.com
- {target} :  https://www.baidu.com



![](./images/2.png)





### 更新日志

#### 1.0.5

感谢 "**咖啡**" 师傅的建议：修改原来的配置文件位置，直接把配置和jar包打包在一个目录。参考：https://github.com/pmiaowu/BurpShiroPassiveScan



#### 1.0.4

新增随机生成信息：https://github.com/smxiazi/xia_Liao



#### 1.0.3.1

1. 感谢 [alex123-2star](https://github.com/alex123-2star) 师傅提交的代码：优化 Mac 快捷启动 和 请求处理（{domain}  {target} ）
2. 如果当前 BurpSuite 目录存在 **DAM 目录和文件 **就会优先访问，但是**不会创建**。其次才访问 `/用户根目录/.config/DAM/` 下的文件（会创建目录和配置文件）



#### 1.0.3

1.0.3 版本所有配置都放在了`/用户根目录/.config/DAM/`，新增了一个快捷启动工具的功能，可以通过设置工具的路径和命令进行快捷启动。Linux 系统需要安装 `gnome-terminal` ，mac 没测试。

该功能主要抄的工具：

https://github.com/bit4woo/knife

https://github.com/kN6jq/gather



#### 1.0.2

1.0.2 版本添加了一个 GUI 方便查看 漏洞 和 Payload



### 参考

本工具基于大量优秀文章和工具才得以~~编写~~ 抄写完成，非常感谢这些无私的分享者！

https://github.com/d3vilbug/HackBar

https://github.com/bit4woo/knife

https://github.com/kN6jq/gather
