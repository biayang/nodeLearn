# **PM2的基本使用**
---
目录
+ [pm2的安装](#1)
+ [更新PM2](#2)
+ [上传项目到服务器并使用普通方式启动](#3)
+ [使用PM2启动项目](#4)
+ [pm2对项目的基本管理](#5)
  + [启动项目](#5.1)
  + [列出PM2管理的所有应用程序](#5.2)
  + [停止项目](#5.3)
    + [停止某个项目](#5.3.1)
    + [停止所有项目](#5.3.2)
  + [重启项目](#5.4)
    + [重启某个项目](#5.4.1)
    + [重启所有项目](#5.4.2)
  + [删除项目进程](#5.5)
    + [删除某个项目进程](#5.5.1)
    + [删除全部项目进程](#5.5.2)
+ [pm2携带参数启动](#6)
+ [查看日志](#7)
  + [默认文件位置](#7.1)
  + [使用命令查看历史文件](#7.2)
  + [常用日志操作命令](#7.3)
+ [pm2查看monit](#8)
+ [pm2使用配置启动项目](#9)
---
<h3 id="1">1.pm2的安装</h3>
pm2是基于npm进行安装的，在安装pm2之前要先安装npm 

      `sudo npm install -y pm2 -g`

查看安装的pm2的版本

命令：

       `sudo pm2 -v`
       
出现下图即安装成功

![pm2安装成功](https://img-blog.csdnimg.cn/20190712235351422.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM2OTM4NjE3,size_16,color_FFFFFF,t_70)

<h3 id="2">2.更新PM2</h3>
更新PM2非常快（少于几秒）并且无缝。

首先确保您正确保存了所有进程：

   `sudo pm2 save`

然后从NPM安装最新的PM2版本：

    sudo npm install pm2 -g

最后更新内存中的PM2进程：

    sudo pm2 update

就是这样，您现在拥有了一个全新的PM2系统
<h3 id="3">3.上传项目到服务器并使用普通方式启动</h3>
使用普通方式启动项目

命令：

       sudo npm start app.js
> 如果你的项目package.json里面的script配置了启动脚本，就执行这个脚本

<h3 id="4">4.使用PM2启动项目</h3>

> ___注意：使用pm2启动项目时，默认是通过自己项目中的package.json中的配置进行启动的，需要查看项目中的package.json中start的配置___
---
使用vim查看package.json文件

命令：

       sudo vim package.json
       
![查看scripts下的start的配置值，根据这个启动路径进行启动。记住这个启动路径，退出查看](https://img-blog.csdnimg.cn/20190713001050904.png)

在项目路径下启动项目

命令：

       sudo pm2 start ./bin/www         //启动当前项目

![](https://img-blog.csdnimg.cn/20190713001059299.png)
<h3 id="5">5.pm2对项目的基本管理</h3>
<h3 id="5.1">5.1启动项目</h3>
> 此处应有其他方法 以后研究的多了再找

<h3 id="5.2">5.2列出PM2管理的所有应用程序</h3>

命令：

       sudo pm2 ls



或者使用list

命令：

       sudo pm2 list
<h3 id="5.3">5.3停止项目</h3>
<h3 id="5.3.1">5.3.1停止某个项目</h3>
指定项目app name或id

命令：

       sudo pm2 stop www           //停止项目名为www的应用程序

或者

       sudo pm2 stop 0         //停止项目id为0的应用程序
       
<h3 id="5.3.2">5.3.2停止所有项目</h3>

命令：

       sudo pm2 stop all        //停止pm2管理的所有应用程序
       
<h3 id="5.4">5.4重启项目</h3>
<h3 id="5.4.1">5.4.1重启某个项目</h3>

使用restart重启指定项目app name或id

命令：

       sudo pm2 restart www        //重启项目名为www的应用程序

或者

       sudo pm2 restart 0             //重启项目id为0的应用程序
       
使用reload重载（重启）指定项目app name或id

命令：

       sudo pm2 reload www        //重载项目名为www的应用程序

或者

       sudo pm2 reload 0             //重载项目id为0的应用程序
       
       
<h3 id="5.4.2">5.4.2重启所有项目</h3>

命令：

       sudo pm2 restart all            //重启pm2管理的所有应用程序

或者

       sudo pm2 reload all            //重载pm2管理的所有应用程序
       
<h3 id="5.5">5.5删除项目</h3>
<h3 id="5.5.1">5.5.1删除某个项目</h3>

在进行删除某个项目进程时，一般通需要先停止一段时间才会在去删除该进程

命令：

       sudo pm2 delete www        //删除项目名为www的应用程序的进程

或者

       sudo pm2 delete 0              //删除项目id为0的应用程序的进程

 
<h3 id="5.5.2">5.5.2删除所有项目</h3>

命令：

       sudo pm2 delete all            //删除pm2管理的所有应用程序的进程
       
<h3 id="6">6.pm2携带参数启动</h3>

```

# 指定应用程序名称
--name <app_name>
 
# 当文件更改时，重启应用程序
--watch
 
# 为应用程序重新加载设置内存阈值
--max-memory-restart <200MB>
 
# 指定日志文件
--log <log_path>
 
# 向脚本传递额外的参数
-- arg1 arg2 arg3
 
# 自动重启之间的延迟
--restart-delay <delay in ms>
 
# 在日志前面加上时间前缀
--time
 
# 不要自动重启应用程序
--no-autorestart
 
# 为强制重启指定cron
--cron <cron_pattern>
 
# 附加到应用程序日志
--no-daemon
```
<h3 id="7">7.查看日志</h3>



