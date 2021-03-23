## v2ray安装

新版安装配置实例
服务端安装
下载安装脚本
>~ curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh  

执行安装脚本
>  ~ bash ./install-release.sh
```bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   98k  100   98k    0     0   495k      0 --:--:-- --:--:-- --:--:--  495k
info: Installing V2Ray v4.27.5 for x86_64
Downloading V2Ray archive: https://github.com/v2fly/v2ray-core/releases/download/v4.27.5/v2ray-linux-64.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   644  100   644    0     0   5457      0 --:--:-- --:--:-- --:--:--  5457
100 12.6M  100 12.6M    0     0  8316k      0  0:00:01  0:00:01 --:--:-- 10.2M
Downloading verification file for V2Ray archive: https://github.com/v2fly/v2ray-core/releases/download/v4.27.5/v2ray-linux-64.zip.dgst
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   649  100   649    0     0   2368      0 --:--:-- --:--:-- --:--:--  2368
100   590  100   590    0     0   1053      0 --:--:-- --:--:-- --:--:--  1053
info: Extract the V2Ray package to /tmp/tmp.gWzZRTMMij and prepare it for installation.
installed: /usr/local/bin/v2ray
installed: /usr/local/bin/v2ctl
installed: /usr/local/share/v2ray/geoip.dat
installed: /usr/local/share/v2ray/geosite.dat
installed: /usr/local/etc/v2ray/config.json
installed: /var/log/v2ray/
installed: /var/log/v2ray/access.log
installed: /var/log/v2ray/error.log
installed: /etc/systemd/system/v2ray.service
installed: /etc/systemd/system/v2ray@.service
removed: /tmp/tmp.gWzZRTMMij
info: V2Ray v4.27.5 is installed.         //安装完成
You may need to execute a command to remove dependent software: dnf remove curl unzip
Please execute the command: systemctl enable v2ray; systemctl start v2ray
```

服务端配置
默认安装完成后，启用配置文件为/usr/local/etc/v2ray/config.json，但这个默认配置为空，因此需要自定义服务端配置。
```json
{
  "inbounds": [{
    "port": 33665,
    "protocol": "vmess",
    "settings": {
      "clients": [
        {
          "id": "e541585f-7c34-4eab-9c08-c1c2ebbd69ed",
          "level": 1,
          "alterId": 64
        }
      ]
    }
  }],
  "outbounds": [{
    "protocol": "freedom",
    "settings": {}
  },{
    "protocol": "blackhole",
    "settings": {},
    "tag": "blocked"
  }],
  "routing": {
    "rules": [
      {
        "type": "field",
        "ip": ["geoip:private"],
        "outboundTag": "blocked"
      }
    ]
  }
}
```


配置systemd服务/启动v2ray 
>  ~ systemctl enable v2ray //添加systemd服务模块
Created symlink /etc/systemd/system/multi-user.target.wants/v2ray.service → /etc/systemd/system/v2ray.service.

>  ~ systemctl start v2ray  //开启v2ray服务

>  ~ service v2ray status  //检查v2ray服务状态
```bash
Redirecting to /bin/systemctl status v2ray.service
● v2ray.service - V2Ray Service
   Loaded: loaded (/etc/systemd/system/v2ray.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2020-09-07 11:16:13 CST; 8s ago
 Main PID: 25897 (v2ray)
    Tasks: 6 (limit: 4566)
   Memory: 4.7M
   CGroup: /system.slice/v2ray.service
           └─25897 /usr/local/bin/v2ray -config /usr/local/etc/v2ray/config.json

Sep 07 11:16:13 bwgcn2 systemd[1]: Started V2Ray Service.
Sep 07 11:16:13 bwgcn2 v2ray[25897]: V2Ray 4.27.5 (V2Fly, a community-driven edition of V2Ray.) Custom (go1.14.7 linux/amd64)
Sep 07 11:16:13 bwgcn2 v2ray[25897]: A unified platform for anti-censorship.
Sep 07 11:16:13 bwgcn2 v2ray[25897]: 2020/09/07 11:16:13 [Info] v2ray.com/core/common/platform/ctlcmd: <v2ctl message>
Sep 07 11:16:13 bwgcn2 v2ray[25897]: v2ctl> Read config:  /usr/local/etc/v2ray/config.json
Sep 07 11:16:13 bwgcn2 v2ray[25897]: 2020/09/07 11:16:13 [Warning] v2ray.com/core: V2Ray 4.27.5 started
```
### win端连接：
下载最新版v2rayN，地址为https://github.com/2dust/v2rayN/releases/download/3.23/v2rayN-Core.zip
#### 1.解压文件后双机打开 v2rayN.exe 文件
![解压文件后双机打开v2rayN.exe文件.png](https://raw.githubusercontent.com/307523005/monster/master/v2ray/解压文件后双机打开v2rayN.exe文件.png)
#### 2.新建服务器添加

![新建服务器添加1.png](https://raw.githubusercontent.com/307523005/monster/master/v2ray/新建服务器添加1.png)
![新建服务器添加2.png](https://raw.githubusercontent.com/307523005/monster/master/v2ray/新建服务器添加2.png)
点击确定
#### 3.正常显示

![正常显示.png](https://raw.githubusercontent.com/307523005/monster/master/v2ray/正常显示.png)
#### 4.右击小图标

![右击小图标.png](https://raw.githubusercontent.com/307523005/monster/master/v2ray/右击小图标.png)

#### 5.选择PAC模式

![选择PAC模式.png](https://raw.githubusercontent.com/307523005/monster/master/v2ray/选择PAC模式.png)

#### 6.浏览器输入 油管网址 http://youtube.com/ 
