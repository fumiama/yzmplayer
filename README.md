# yzmplayer
仿bilibili的m3u8弹幕播放器

# 使用准备
以`Ubuntu`为例
### 1. 安装php7.x
```bash
sudo apt-get install php
```
### 2. 安装apache2
`Ubuntu`自带`apache2`
### 3. 安装mysql并配置
```bash
sudo apt-get install mysql-server
sudo mysql_secure_installation
sudo service mysql start
```
### 4. 安装php-curl php-xml php-xmlrpc
```bash
sudo apt-get install php-curl php-xml php-xmlrpc
```
### 5. 编辑apache2/php.ini
```bash
sudo vi /etc/php/7.2/apache2/php.ini
```
取消注释`curl`与`mysqli`，并添加一行在`extension=mysqli`前
```bash
extension=curl
...
extension=mysqlnd
extension=mysqli
```

# 使用方法
1. 解压到网站根目录
2. 访问 你的域名/dmku 进行配置数据库  
3. 修改播放器后台密码 dmku/config.inc.php
4. 登录后台 你的域名/admin 密码为第3步修改的密码
5. 播放器功能可后台设置

# 参数说明（player/index.php）
"av":'<?php echo($_GET['av']);?>',//B站av号，用于调用弹幕
"url":"<?php echo($_GET['url']);?>",//视频链接
"id":"<?php echo($_GET['url']);?>",//视频id
"sid":"<?php echo($_GET['sid']);?>",//集数id
"pic":"<?php echo($_GET['pic']);?>",//视频封面
"title":"<?php echo($_GET['name']);?>",//视频标题
"next":"<?php echo($_GET['next']);?>",//下一集链接
"user": '<?php echo($_GET['user']);?>',//用户名
"group": "<?php echo($_GET['group']);?>",//用户组

# 请求示例
#### 基本
http://localhost/player/?url=https://cdn.jsdelivr.net/gh/MoGuJ/Video-Bed/Your.Name/playlist.m3u8

#### 高级
除了 url 参数，其他都可以省略

http://localhost/player/?url=https://cdn.jsdelivr.net/gh/MoGuJ/Video-Bed/Your.Name/playlist.m3u8&next=https://cdn.jsdelivr.net/gh/MoGuJ/Video-Bed/Your.Name/playlist.m3u8&sid=1&pic=https://img.xx.com/1.png&user=游客&group=1&name=测试

# 修改记录
> 原作者：京都一只喵，蘑菇君做了一些小修复

1. 解密 `yzmplayer.js` 文件
2. 修复了视频弹幕非独立的问题
3. 兼容了 PHP7.X，在 PHP7.4 环境测试通过
4. 更新版本号至 v1.2.1
5. 重写了使用说明

> 2020年7月泽泽

1，修复弹幕后台管理登录系统后门（原版居然将正确密码存cookie里了）
2，修复安装程序界面没有样式问题
3，后台登录支持输出账号与密码了，更改用户名与密码请修改dmku文件夹下的config.inc.php文件
