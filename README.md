Pico设备搭梯子 简易教程（也可用于手机、电脑）
A simple guide for how to connect VPN on Pico device.

教程分三部分：
一、获得海外服务器账号
很多网站可以购买到海外服务器。各位可以按照性价比选择网站及设备。
在此以 https://my.vultr.com/ 购买的服务器举例：vultr网站可靠性比较高，最低配置服务器足够两个人日常使用，平均每个月35元。弹性服务器服务器，可以随时停掉或换新，按小时收费。
1.首先注册并登录账号
2.在左侧栏中选择Billing并充值10美刀（2021.6.10大概人民币65元左右，首月应该还会有优惠，我的账户比较老所以截图里不包括优惠活动）
![image](https://user-images.githubusercontent.com/25834609/121460085-f0836e00-c9de-11eb-8fc0-3f45178ae4f1.png)
3.在左侧栏中选择Products鼠标移到+号并选择Deploy New Server
![image](https://user-images.githubusercontent.com/25834609/121460341-6091f400-c9df-11eb-93f9-e440a28d169e.png)
4.choose server选择 cloud compute ，服务器地区尽量选择离自己地理位置较近的（实测新加坡最好但经常会被抢光，其次是日本，日本服务器在部分地区效果不是很好，如果效果不好可以删除并选择其他地区服务器，服务器按小时付费所以更换损失不大），Server Type选择CentOS. Server Size选择5美元一个月即可。其他均不需改动并点击右下角Deploy Now即可。
![image](https://user-images.githubusercontent.com/25834609/121461074-b915c100-c9e0-11eb-80b0-02bea2b3ffb7.png)
![image](https://user-images.githubusercontent.com/25834609/121461105-c9c63700-c9e0-11eb-8332-3201cb87cbd1.png)
5.返回Products会发现有一台正在创建的服务器，等待1分钟左右变成Running状态
![image](https://user-images.githubusercontent.com/25834609/121462595-6be71e80-c9e3-11eb-8124-da78464c05b3.png)
![image](https://user-images.githubusercontent.com/25834609/121461252-127df000-c9e1-11eb-9e9a-b4b4750286c2.png)
6.点击服务器进入详情查看页，可以看到服务器相关的一些信息，最主要是IP Address和Password，也就是服务器账号密码
二、对服务器进行初始配置
0.首先看看自己的服务器可否正常，打开Mac终端或windows命令提示符输入ping + 你的服务器账户名，如果出现以下图则为正常状态
![image](https://user-images.githubusercontent.com/25834609/121462836-d0a27900-c9e3-11eb-817b-d1754c75d070.png)
如果一直出现times out则服务器异常，建议删除重新建。
1.首先需要远程进入自己的服务器，需要用到SSH工具，如果你是Mac用户，可以直接用系统自带的终端连接，输入账号点击连接，进入窗口看到password后粘贴自己的密码回车即可成功进入
![image](https://user-images.githubusercontent.com/25834609/121462395-1d398480-c9e3-11eb-84e0-362c24dc4d08.png)

（如果你是windows用户，可自行上网搜索SSH工具及使用教程。输入账号密码进行连接）
2.基础配置，网上大部分教程配置过程叫复杂，可以尝试脚本工具，在服务器中
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ss-go.sh && chmod +x ss-go.sh && bash ss-go.sh
![image](https://user-images.githubusercontent.com/25834609/121466244-af448b80-c9e9-11eb-9357-053b25ee1bcb.png)
输入1并回车安装shadowsocks
端口号直接回车，密码粘贴服务器密码即可，加密方式选择aes-256-gcm对应选项，其他均默认回车即可，配置成功！
![image](https://user-images.githubusercontent.com/25834609/121467205-478f4000-c9eb-11eb-9464-b9b7e084c690.png)
3.KCPtun加速，会大幅加速服务器（还起到了避免服务器被封的作用，比较重要）
分别运行如下三条命令
wget --no-check-certificate https://github.com/kuoruan/shell-scripts/raw/master/kcptun/kcptun.sh
chmod +x ./kcptun.sh
./kcptun.sh
（以下截图自https://ssr.tools/588，需要VPN）
![image](https://user-images.githubusercontent.com/25834609/121467251-5aa21000-c9eb-11eb-80b7-4eefc8ea4c98.png)
![image](https://user-images.githubusercontent.com/25834609/121467265-6097f100-c9eb-11eb-9e28-f84fed202080.png)
![image](https://user-images.githubusercontent.com/25834609/121467283-68579580-c9eb-11eb-994b-1cc15341d3b5.png)
![image](https://user-images.githubusercontent.com/25834609/121467300-6db4e000-c9eb-11eb-935b-9f1fa20963f9.png)
![image](https://user-images.githubusercontent.com/25834609/121467332-77d6de80-c9eb-11eb-8465-46342693063f.png)
![image](https://user-images.githubusercontent.com/25834609/121467366-7efdec80-c9eb-11eb-8f55-7f80c6fce2c5.png)
![image](https://user-images.githubusercontent.com/25834609/121467422-9c32bb00-c9eb-11eb-98be-05814a0ddc82.png)
三、下载并配置SSR
1.先在电脑端配置SSR https://github.com/search?q=shadowsocks
![image](https://user-images.githubusercontent.com/25834609/121467891-896cb600-c9ec-11eb-94ea-068558cdc818.png)
（进入后在右侧Releases找到最新版本下载)
解压后打开，以下以mac为例，windows可以对应百度
![image](https://user-images.githubusercontent.com/25834609/121468123-e1a3b800-c9ec-11eb-839d-a6cc7aa118fd.png)
填入对应的刚才设置的参数，点击保存，启动shadowsocks之后如果可以成功访问谷歌，则配置成功。
![image](https://user-images.githubusercontent.com/25834609/121468215-013ae080-c9ed-11eb-9d09-3ac0ce54561c.png)
2.下载最新版本安卓端APK https://github.com/shadowsocks/shadowsocks-android/releases/tag/v5.2.3 ，并拷贝到Pico头戴设备中解压
从电脑端点击导出服务器到剪贴板
![image](https://user-images.githubusercontent.com/25834609/121468528-81614600-c9ed-11eb-8f3b-c19e366f51b9.png)
需要将这条消息复制到Pico设备中：可以通过firfox浏览器邮件，也可以通过抖音发消息然后Pico端复制，方法不限
打开Pico端shadowsocks之后选择右上角➕，点击从剪贴板导入，即可导入配置好的服务器。
点击返回键（不要点击退出键）即可
