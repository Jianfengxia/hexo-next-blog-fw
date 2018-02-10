---
title: "paramiko远程连接ssh2 - Python自动化运维"
date: 2017-06-30 08:00:00
updated: 2017-06-22 09:23:37
tags: ["Python"]
---
paramiko是用python语言写的一个模块，遵循SSH2协议，支持以加密和认证的方式，进行远程服务器的连接。

由于使用的是python这样的能够跨平台运行的语言，所以所有python支持的平台，如Linux, Solaris, BSD, MacOS X,Windows等，paramiko都可以支持，因此，如果需要使用SSH从一个平台连接到另外一个平台，进行一系列的操作时，paramiko是最佳工具之一。  

  
1. 安装Pip & Python 2.7 (or 3.6),并配置环境变量(默认安装会自动添加)
2. 设置Notepad++作为IDE开发工具:运行中输入命令cmd /k python "$(FULL_CURRENT_PATH)" & ECHO. & PAUSE & EXIT
3. 安装第三方库: pip install paramiko

Examples:
 
```python
 # -- coding: utf-8 --

 #!/usr/bin/env python

 import paramiko

 

 hostname='10.1.134.128'

 username='username'

 password='password'

 #paramiko.util.log_to_file('syslogin.log')

    

    ssh=paramiko.SSHClient()

    #ssh.load_system_host_keys()

    ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())

    ssh.connect(hostname=hostname,username=username,password=password)

    stdin,stdout,stderr=ssh.exec_command('free -m')

    print stdout.read()

    ssh.close()

  

  
