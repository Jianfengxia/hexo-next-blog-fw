---
title: "使用Hexo + Next搭建静态博客"
date: 2017-07-05 08:00:00
updated: 2017-06-29 08:58:44
tags: ["Python","JavaScript"]
---
**目的：**
[Github](https://github.com/) \+ Hexo + Next + 域名搭建可自定义前端样式的免费博客
  * 超快速度： Node.js 所带来的超快生成速度，让上百个页面在几秒内瞬间完成渲染。
  * 支持 Markdown： Hexo 支持 GitHub Flavored Markdown 的所有功能，甚至可以整合 Octopress 的大多数插件。
  * 一键部署： 只需一条指令即可部署到 GitHub Pages, Heroku 或其他网站。
  * 丰富的插件： Hexo 拥有强大的插件系统，安装插件可以让 Hexo 支持 Jade, CoffeeScript。
  
**准备：**
GitHub账号申请  
新建一个仓库（new repository），并命名为YourSiteName.github.io
用一键安装包安装nodejs环境 - <http://nodejs.cn/download/>
安装git工具 - <https://git-scm.com/downloads>
  
**部署:**
  1. 使用npm安装hexo - 命令行$ npm install -g hexo-cli
  2. 初始化框架 - 命令行$ hexo init| cd| npm install
  3. 新建文章（创建一个Hello World） - 命令行$ hexo new "Hello World" (该命令在/source/_post里添加hello-world.md文件，之后新建的文章都将存放在此目录下。)
  4. 新建关于我等相关页面 \- 命令行$ hexo new page "about" (该命令在/source/about里添加index.md文件)  
  5. 生成网站 命令行$ hexo generate 或者 $ hexo g (此时会将/source的.md文件生成到/public中，形成网站的静态文件。)
  6. 使用Next主题让站点更酷炫, 下载https://github.com/iissnan/hexo-theme-next 并放入项目根目录下的themes/next (可修改该模板中的内容或替换相关图片)
  7. 在source文件夹中新增CNAME,404.html等固定页面  
  8. 启用模板, 需要修改根目录/_config.yml配置项theme: next
  9. 验证是否启用 $ hexo s --debug, 如显示theme: next则为成功,默认是theme: landscape
  10. Ctrl+C退出debug, 正常启动服务器 - 命令行$ hexo server 或者 $ hexo s (输入http://localhost:4000即可查看网站。)  
  11. 部署网站 - $ hexo deploy 或者 $ hexo d, 部署网站之前需要生成静态文件，即可以用$ hexo generate -d直接生成并部署。此时需要在_config.yml中配置你所要部署的站点：
 
 
 ## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: git
       repo: git@github.com:YourRepository.git
       branch: master
  
  
**更多:**  
Hexo配置参考: <https://github.com/Jianfengxia/hexo-next-blog-fw/blob/master/_config.yml>
Next配置参考: <https://github.com/Jianfengxia/hexo-next-blog-fw/blob/master/themes/next/_config.yml>
404页面配置参考: <https://github.com/Jianfengxia/hexo-next-blog-fw/blob/master/source/404.html>
CNAME域名配置参考:<https://github.com/Jianfengxia/hexo-next-blog-fw/blob/master/source/CNAME>
官网[[Next]](http://theme-next.iissnan.com/)  
[[Hexo | 配置]](https://hexo.io/zh-cn/docs/configuration.html)
[[Hexo | 指令]](https://hexo.io/zh-cn/docs/commands.html)
[[Next | 主题设定]](http://theme-next.iissnan.com/theme-settings.html)
[[Next | 第三方服务]](http://theme-next.iissnan.com/third-party-services.html)
那么到此为止网站的雏形算是完成了，接下来你就要自己去管理和完善个人网站了。
