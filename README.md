# BTinstall_6.0
宝塔面板7.7原版安装脚本

宝塔面板7.8版本使用各种方法均无法绕过绑定账号，并且不绑定账号无法下载安装插件。

因此这里分享一下7.7版本的安装脚本，是官方免费版的。
```
wget -O install.sh https://raw.githubusercontent.com/insoxin/BTinstall_6.0/main/install_6.0.sh && bash install.sh
```

升级到7.7版本命令：
curl http://f.cccyun.cc/bt/update6.sh|bash


建议配合下面文章中的优化脚本使用：
这个是自用的宝塔面板一键优化补丁，主要有以下优化项目：

1.去除宝塔面板强制绑定账号

2.去除各种删除操作时的计算题与延时等待

3.去除创建网站自动创建的垃圾文件（index.html、404.html、.htaccess）

4.关闭未绑定域名提示页面，防止有人访问未绑定域名直接看出来是用的宝塔面板

5.关闭活动推荐与在线客服

6.去除自动校验文件与上报信息定时任务

7.去除面板日志与网站绑定域名上报

```
手动破解：
1，屏蔽手机号

sed -i "s|bind_user == 'True'|bind_user == 'XXXX'|" /www/server/panel/BTPanel/static/js/index.js
2，删除强制绑定手机js文件

rm -f /www/server/panel/data/bind.pl
3，手动解锁宝塔所有付费插件为永不过期

文件路径：/www/server/panel/data/plugin.json

搜索字符串："endtime": -1全部替换为"endtime": 999999999999

4，给plugin.json文件上锁防止自动修复为免费版

chattr +i /www/server/panel/data/plugin.json
============================

！！如需取消屏蔽手机号

sed -i "s|if (bind_user == 'REMOVED') {|if (bind_user == 'True') {|g" /www/server/panel/BTPanel/static/js/index.js
