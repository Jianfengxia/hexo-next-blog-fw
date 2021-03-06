---
title: "Saltstack之state配置管理"
date: 2017-07-04 09:00:00
updated: 2017-07-19 10:10:35
tags: ["Python","运维","Saltstack"]
---
  
# **state模块简介**
  
**state功能**  
state是Saltstack最核心的功能，通过预先定制好的sls（salt state file）文件对被控制主机进行状态管理，支持包括程序包（pkg）、
文件（file）、网络配置（network）、系统服务（service）、系统用户（user）等。
  
**state的定义**
state是通过sls文件进行描述的，支持YAML语法，定义规则如下：
 
 
 $ID: #定义state名称，通常采用与描述对象保存一致的方法，如apache、nginx等 
$state: #须管理对象的类型
        - $state: states #定制对象的状态
  

 
ache: #state名称：apache
pkg: #管理对象类型：pkg，进行软件安装（yum、apt）
 installed #pkg要执行的方法：install，如未安装就进行安装
      service: #管理对象类型：service，管理系统守护进程
        - running #service要执行的方法：running，如未运行就进行启动
     - require: #关键字require，确保apache服务只有在成功安装软件包后才会启动
       - pkg: apache
  
注：---关键字说明
    
    
    require：在运行此state之前，先运行依赖的state关系检查，可配置多个state依赖对象；
    watch：在检查摸个state发生变化时运行此模块。

**state的使用**
state的入口文件与pillar一样，文件名都是top.sls，但state要求sls文件必须存放在Saltstack
base定义的目录下（默认为/srv/salt）。
state描述配置*.sls支持jinjia模板、grains及pillar引用等，在state的逻辑层次定义完成后，再通过salt '*'
state.highstate执行生效。
  
  
*结合grains与pillar，实现一个根据不同操作系统类型部署apache环境的任务**  

**定义pillar**  
【/srv/pillar/top.sls】
    
    
    base:
   '*':
     - apache
ls中引用二级配置有两种方式，一种是直接引用，如本例中直接引用apache.sls；另一种是创建apache目录，再引用目录中的init.sls
果是一样的。

rv/pillar/apache.sls】或【/srv/pillar/apache/init.sls】
    
    
 pkgs:
 { % if grains['os_family'] == 'Debian' % }
      apache: apache2
      { % elif grains['os_family'] == 'RedHat' % }
      apache: httpd
      { % elif grains['os'] == 'Arch' % }
      apache: apache
    { % endif % }


    salt '*' saltutil.refresh_pillar #刷新pillar
    salt '*' pillar.data pkgs #获取pkgs信息
  


ate**
salt/top.sls】

    
    base:
      '*':
     - apache
  
【/srv/salt/apache.sls】或【/srv/salt/apache/init.sls】
    
    
    apache:
      pkg:
        - installed
        - name: {{ pillar['pkgs']['apache'] }} #pillar['pkgs']['apache']引用的是pillar定义的数据
      service.running:
        - name: {{ pillar['pkgs']['apache'] }}
        - require:
          - pkg: {{ pillar['pkgs']['apache'] }}
  
**执行state**
    
    
    salt '*' state.highstate
  
