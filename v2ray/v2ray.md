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

### 最后贴出几个免费的服务器连接
```bash
ss://YWVzLTI1Ni1nY206eHBRd3lWNFc1RmRBNk5NQU5KSng3M1VTQDIuNTguMjQyLjQzOjM4MDMz#%E5%8F%B0%E6%B9%BE1(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
ss://YWVzLTI1Ni1nY206eHBRd3lWNFc1RmRBNk5NQU5KSng3M1VTQDIuNTguMjQxLjQzOjM4MDMz#%E5%8F%B0%E6%B9%BE2(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
ss://YWVzLTI1Ni1nY206OG42cHdBY3JydjJwajZ0RlkycDNUYlE2QDE2NS4yMzEuMjUzLjE0NzozMzk5Mg==#%E5%8F%B0%E6%B9%BE3(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
ss://YWVzLTI1Ni1nY206OG42cHdBY3JydjJwajZ0RlkycDNUYlE2QDE5My45LjExMi4xOTU6MzM5OTI=#%E6%AC%A7%E6%B4%B2(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
ss://YWVzLTI1Ni1nY206OG42cHdBY3JydjJwajZ0RlkycDNUYlE2QDM3LjEyMC4yMTIuMTQ5OjMzOTky#%E6%AC%A7%E6%B4%B21(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
ss://YWVzLTI1Ni1nY206OG42cHdBY3JydjJwajZ0RlkycDNUYlE2QDM3LjEyMC4yMTIuMTQ3OjMzOTky#%E6%AC%A7%E6%B4%B22(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
ss://YWVzLTI1Ni1nY206OG42cHdBY3JydjJwajZ0RlkycDNUYlE2QDE5OC44Ljg1LjgyOjMzOTky#%E7%BE%8E%E5%9B%BD(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
ss://YWVzLTI1Ni1nY206OG42cHdBY3JydjJwajZ0RlkycDNUYlE2QDE5OC44Ljg1Ljg5OjMzOTky#%E7%BE%8E%E5%9B%BD1(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
ss://YWVzLTI1Ni1nY206OG42cHdBY3JydjJwajZ0RlkycDNUYlE2QDE5OC44Ljg1LjEzMzozMzk5Mg==#%E7%BE%8E%E5%9B%BD2(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIue+juWbvTMoWW91dHViZemikemBk++8muW3peWFt+Wkp+W4iGkpIiwNCiAgImFkZCI6ICIxMDQuMjcuMTM5LjIxOSIsDQogICJwb3J0IjogIjQ0MyIsDQogICJpZCI6ICIzYjVlMjU4ZS04YzVlLTQ1ZDMtYjdkMi0wMmM4ZjVmYzBiYjIiLA0KICAiYWlkIjogIjY0IiwNCiAgIm5ldCI6ICJ3cyIsDQogICJ0eXBlIjogIm5vbmUiLA0KICAiaG9zdCI6ICJhaHZ1eGZxLm9xbnFyeXNhLmNvbSIsDQogICJwYXRoIjogIi8iLA0KICAidGxzIjogInRscyINCn0=
ss://YWVzLTI1Ni1nY206OG42cHdBY3JydjJwajZ0RlkycDNUYlE2QDE5OC44Ljg1LjQwOjMzOTky#%E7%BE%8E%E5%9B%BD4(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIue+juWbvTUoWW91dHViZemikemBk++8muW3peWFt+Wkp+W4iGkpIiwNCiAgImFkZCI6ICIxNDEuMTAxLjExNS4xNyIsDQogICJwb3J0IjogIjQ0MyIsDQogICJpZCI6ICI5ZTZjZWVmZi0yNTQ2LTM2OTAtYWMwMC02ZmNkZjMxZGVjOTQiLA0KICAiYWlkIjogIjIiLA0KICAibmV0IjogIndzIiwNCiAgInR5cGUiOiAibm9uZSIsDQogICJob3N0IjogImZyZWV1cy5tY2FuLnRlY2giLA0KICAicGF0aCI6ICIveTI4NCIsDQogICJ0bHMiOiAidGxzIg0KfQ==
ss://YWVzLTI1Ni1jZmI6ZUlXMERuazY5NDU0ZTZuU3d1c3B2OURtUzIwMXRRMERAMTcyLjEwNC4zNC4zMTo4MDk5#%E6%96%B0%E5%8A%A0%E5%9D%A1(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIuiNt+WFsDEoWW91dHViZemikemBk++8muW3peWFt+Wkp+W4iGkpIiwNCiAgImFkZCI6ICIxNTQuODQuMS4xOTIiLA0KICAicG9ydCI6ICI0NDMiLA0KICAiaWQiOiAiNDM2ZjE4OTctNjIyOC00NWFhLThlMmUtOGZlMDMxODI3ODg3IiwNCiAgImFpZCI6ICI2NCIsDQogICJuZXQiOiAid3MiLA0KICAidHlwZSI6ICJub25lIiwNCiAgImhvc3QiOiAid3d3LjEzNjEyNjE3Lnh5eiIsDQogICJwYXRoIjogIi9mb290ZXJzIiwNCiAgInRscyI6ICJ0bHMiDQp9
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIuiNt+WFsDIoWW91dHViZemikemBk++8muW3peWFt+Wkp+W4iGkpIiwNCiAgImFkZCI6ICIxNTQuODQuMS43MCIsDQogICJwb3J0IjogIjQ0MyIsDQogICJpZCI6ICJkZGY5ZTYyNi04YTMyLTQ5ZDItOTc0Yi1hYzMyZGQxNzE0NmEiLA0KICAiYWlkIjogIjY0IiwNCiAgIm5ldCI6ICJ3cyIsDQogICJ0eXBlIjogIm5vbmUiLA0KICAiaG9zdCI6ICJ3d3cuNjQ5NzgzNjAueHl6IiwNCiAgInBhdGgiOiAiL2Zvb3RlcnMiLA0KICAidGxzIjogInRscyINCn0=
ss://YWVzLTI1Ni1nY206bjh3NFN0bmJWRDlkbVhZbjRBanQ4N0VBQDE2NS4yMzEuMTYzLjE5OjMxNTcy#%E6%AC%A7%E6%B4%B2%E6%96%B0(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
ss://YWVzLTI1Ni1nY206OG42cHdBY3JydjJwajZ0RlkycDNUYlE2QDIuNTguMjQxLjU6MzM5OTI=#%E5%8F%B0%E6%B9%BE%E6%96%B0(Youtube%E9%A2%91%E9%81%93%EF%BC%9A%E5%B7%A5%E5%85%B7%E5%A4%A7%E5%B8%88i)
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIummmea4r+aWsChZb3V0dWJl6aKR6YGT77ya5bel5YW35aSn5biIaSkiLA0KICAiYWRkIjogIjEyNC45MC4xNjUuNjIiLA0KICAicG9ydCI6ICIzMDAxMCIsDQogICJpZCI6ICJmZDAwOTI3YS1iMGMyLTQ2MjktYWVmNy1kOWZmMTVhOWQ3MjIiLA0KICAiYWlkIjogIjE2IiwNCiAgIm5ldCI6ICJ3cyIsDQogICJ0eXBlIjogIm5vbmUiLA0KICAiaG9zdCI6ICIiLA0KICAicGF0aCI6ICIvd2Vic29ja2V0IiwNCiAgInRscyI6ICIiDQp9
```