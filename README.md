# TangSengDaoDao
TangSengDaoDao docker 

https://baijiahao.baidu.com/s?id=1773752696554616414&wfr=spider&for=pc

NAS轻松部署自己的即时通讯—唐僧叨叨，八年时间打造
熊猫不是猫QAQ
2023-08-09 19:59四川
  

前言

该项目为群友提供让我折腾一下。项目名字很有趣，叫唐僧叨叨。一款非微信专家，非腾讯专家，历时八年时间打造的运营级别的开源即时通讯聊天软件，采用的是WuKongIM提供通讯动力。看介绍还是蛮不错的，但还是有很多雷区，这些我不提，先跟着熊猫的节奏部署一下看看效果吧！
部署

项目部署很简单，而且作者也给到了部署方法，熊猫也只是将就着方法换成NAS部署的形式。按照作者的方式，我们首先需要在docker文件夹中新建一个tsdd文件夹，随后在该文件下新建一个docker-compose.yaml文件，文件内容按照自己情况更改：

将次文件放入新建的tsdd文件夹中，紧接着我们还需要创建一个.env配置文件，文件内容如下：


其中我们需要更改一些内容，EXTERNAL_IP：服务器的对外IP地址；MYSQL_ROOT_PASSWORD: mysql数据库的root用户密码，随机填写；MINIO_ROOT_PASSWORD： minio 文件服务的密码，随机填写；TS_SMSCODE为手机注册默认的短信验证码。再将该文件也放入tsdd文件夹下。
目录树

最后我们打开群晖的SSH端口，并通过SSH工具链接到群晖。在获取了管理员权限后，我们cd到项目目录下输入命令docker-compose up -d启动项目。
命令行

中间会出现一些报错，提示找不到文件夹，我们按照它给出的提示，新建好对应的文件夹就可以了。需要在tsdd文件夹中分别新建miniodata、mysqldata、wukongim以及tsdd文件夹。随后再次输入命令，就能看到项目部署成功了。
重启项目
体验

浏览器输入http://122.116.7.123:822

就可以看到登录界面了。
登录界面

该项目需要先在手机端注册才能在web端使用，去官方下载好app登录页面长按“欢迎登录唐僧叨叨”这是一个隐藏的注册入口，点击进入注册页面，输入手机号，默认验证码为：123456即可 (不用点获取验证吗)
服务器输入

curl -H "package: com.xinbida.tangsengdaodao" -H "os: Android" -H "appid: wukongchat" -H "model: 22041216C" -H "version: 1.0" -H "Content-Type: application/json; charset=UTF-8" -H "User-Agent: okhttp/5.0.0-alpha.2" -X POST -d '{"password":"111111","code":"123456","zone":"0086","phone":"1111","name":"","device":{"device_name":"Redmi 22041216C","device_id":"c31c6422135548ab","device_model":"22041216C"}}'  "http://122.116.7.197:8090/v1/user/register"
