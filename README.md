### ***使用 GitHub Actions 推送 Hostloc 新帖到TG群组/个人***

###### 简介：

推送效果：https://rss.vipkj.net/

推送源码来自：https://github.com/w2r/hostloc2tg


####### 更新说明。
20.20.7.24 修改为使用Secrets 储存密匙增加安全性。

20.20.7.24 修改为6小时重新运行一次。

2020.07.20 网站加了js验证，针对js验证进行更新，采取抓取手机版的方法绕过js验证

###### GitHub Actions 使用说明：
Fork 本仓库 

1.然后点击你的仓库右上角的 Settings 

2.找到左边 Secrets 这一项，添加2个秘密环境变量。

POST_URL 内容填写TG机器人密匙

TG_ID 内容填写群组ID或者个人ID



![](https://cdn.jsdelivr.net/gh/lzw981731/img/2020/07/24/ccea.png)

![](https://cdn.jsdelivr.net/gh/lzw981731/img/2020/07/24/a9e7.png)

###### VPS 使用说明：
本脚本为python3脚本，需依赖环境requests，lxml，torequests，js2py等库，第74行bot api需要改为自己bot api，118行需要修改推送id, 机器人每20秒更新一次

**需要注册tg机器人，若要推送到频道，请将机器人添加到频道，并给予管理员权限**

###### ht.sh文件说明：

由于hostloc有时开启防御模式，导致部分国外ip无法访问hostloc，getupdate错误导致掉线，后台运行一个自动重新连接脚本

使用方法：linux添加定时任务，**ht.sh存放在root目录下**，注意，ht脚本里的里需要修改为你的hostloc_tg.py的路径（**可不用设置后台运行，目前程序改版，解决了getupdate问题**）

~~~
*/30 * * * * /root/ht.sh
~~~
后台脚本内容：

~~~
#!/bin/bash
# 30分钟判断一次进程是否存在，如果不存在就启动它
# python3请使用全路径，否则可能出现无法启动
PIDS=`ps -ef |grep hostloc_tg |grep -v grep | awk '{print $2}'`
if [ "$PIDS" != "" ]; then
	echo "myprocess is running!"
else
	echo "未发现程序后台运行，正在重启中！"
	/usr/bin/python3 /root/hostloc_tg.py &
fi
~~~

效果图：

![](https://cdn.jsdelivr.net/gh/lzw981731/img/2020/07/24/407b.png)


