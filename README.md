## 诺兰方舟

</br>

更新时间：2022-1-21


原Nvjdc作者，由于ID被抢注，已更名为诺兰方舟(ARK)，Github其他ID均为假冒

* [@NNNNolan](https://github.com/NNNNolan) 



## 注意

```
防狗乱咬

防止泛滥没有许可 用不了 许可自行进作者tg群获取
```

## Docker安装

</br>

### 1.git安装

有些人没有安装，防止拉不到源码

```
yum install git
```

</br>


### 2.拉取源码

```
git clone https://ghproxy.com/https://github.com/Yiov/Ark.git /root/Ark
```

</br>

### 3.拉取镜像

```
docker pull yiov/ark:latest
```

</br>

### 4.安装unzip

```
yum install wget unzip -y
```

</br>

### 5.创建目录下载配置文件

```
cd /root/Ark
mkdir -p  Config && cd Config
```

进宝塔ark文件夹-Config，新建`config.json`文件，粘贴下面代码保存

```
{
  ///浏览器最多几个网页
  "MaxTab": "4",
  //网站标题
  "Title": "Ark",
  //回收时间分钟 不填默认3分钟
  "Closetime": "5",
  //不要修改
  "Captchaurl": "http://127.0.0.1:5000",
  //网站公告
  "Announcement": "为提高账户的安全性，请关闭免密支付。",
  //Proxy 支持不带密码的socks5 以及http 
  ///http  Proxy 只需要填写 ip:端口
  /// Socks5 需要填写socks5://ip:端口 不能填写下方账户密码 或者 socks5://用户名:密码@ip:端口
  "Proxy": "",
  //Proxy帐号
  "ProxyUser": "",
  //Proxy密码
  "ProxyPass": "",
  ///开启打印等待日志卡短信验证登陆 可开启 拿到日志群里回复 默认不要填写
  "Debug": "",
  ///自动滑块次数5次 5次后手动滑块 可设置为0默认手动滑块
  "AutoCaptchaCount": "5",
  ///XDD PLUS Url  http://IP地址:端口/api/login/smslogin
  "XDDurl": "",
  ///xddToken
  "XDDToken": "",
  ///登陆预警 0 0 12 * * ?  每天中午十二点 https://www.bejson.com/othertools/cron/ 表达式在线生成网址
  "ExpirationCron": " 0 0 12 * * ?",
  ///个人资产 0 0 10,20 * * ?  早十点晚上八点
  "BeanCron": "0 0 10,20 * * ?",
  // ======================================= WxPusher 通知设置区域 ===========================================
  // 此处填你申请的 appToken. 官方文档：https://wxpusher.zjiecode.com/docs
  // WP_APP_TOKEN 可在管理台查看: https://wxpusher.zjiecode.com/admin/main/app/appToken
  // MainWP_UID 填你自己uid
  ///这里的通知只用于用户登陆 删除 是给你的通知
  "WP_APP_TOKEN": "",
  "MainWP_UID": "",
  // ======================================= pushplus 通知设置区域 ===========================================
  ///Push Plus官方网站：http" //www.pushplus.plus  只有青龙模式有用
  ///下方填写您的Token，微信扫码登录后一对一推送或一对多推送下面的token，只填" "PUSH_PLUS_TOKEN",
  "PUSH_PLUS_TOKEN": "",
  //下方填写您的一对多推送的 "群组编码" ，（一对多推送下面->您的群组(如无则新建)->群组编码）
  "PUSH_PLUS_USER": "",
  ///青龙配置  注意对接XDD 对接芝士 设置为"Config":[]
  "Config": [
    {
      //序号必填从1 开始
      "QLkey": 1,
      //服务器名称
      "QLName": "阿里云",
      //青龙地址
      "QLurl": "http://ip:5700",
      //青龙-系统设置-应用设置-添加应用，名称随意，权限全给
      "QL_CLIENTID": "",
      //青龙-系统设置-应用设置-添加应用，名称随意，权限全给
      "QL_SECRET": "",
      //CK最大数量
      "QL_CAPACITY": 99,
      ///建议一个青龙一个WxPusher 应用
      "WP_APP_TOKEN": ""
    }
  ]

}
```

</br>


### 6.创建子文件夹下载chromium

回到nolanjdc目录，创建chromium文件夹并进入

```
cd /root/Ark && mkdir -p  .local-chromium/Linux-884014 && cd .local-chromium/Linux-884014
```

```
wget https://mirrors.huaweicloud.com/chromium-browser-snapshots/Linux_x64/884014/chrome-linux.zip && unzip chrome-linux.zip
```

删除下载chrome的压缩包，并回到nolanjdc目录

```
rm  -f chrome-linux.zip
cd  /root/Ark
```

</br>


### 7.创建容器


代码中的 `-p 5602:80`，5602端口可以自己改，80不要动

> 注意 5000端口可以不开外网端口

```
sudo docker run -d \
--name ark \
-p 5602:80 \
-p 5000:5000 \
-v  "$(pwd)":/app/Ark \
-v /etc/localtime:/etc/localtime:ro \
-it --privileged=true \
yiov/ark:latest
```

</br>


### 8.查看是否成功

没有许可不可用，请自行获取

```
docker logs -f ark
```
</br>


### 9.重启容器

```
docker restart ark
```

</br>

### 10.访问前端

你的公网ip加你的端口，如果按照本教程来的默认5602，如果自己改过按照你改的来

如：http://192.168.1.110:5602


</br>




## 拓展使用


</br>

### 拓展1：更新


以后更新按这个步骤走，不需要删镜像

```
cd /root/ark
docker stop ark
```

```
git pull
```

```
docker start ark
```

</br>



### 拓展2：删除配置

```
docker rm -f ark #删除容器
docker rmi -f yiov/ark:latest #删除镜像
在宝塔删除ark整个文件夹 #删除所有配置
```
</br>




### 拓展3：多开容器

```
{
  ///浏览器最多几个网页
  "MaxTab": "4",
  //网站标题
  "Title": "NolanJDCloud",
  //回收时间分钟 不填默认3分钟
  "Closetime": "5",
  //网站公告
  "Announcement": "为提高账户的安全性，请关闭免密支付。",
  ///开启打印等待日志卡短信验证登陆 可开启 拿到日志群里回复 默认不要填写
  "Debug": "",
  ///自动滑块次数5次 5次后手动滑块 可设置为0默认手动滑块
  "AutoCaptchaCount": "0",
  ///XDD PLUS Url  http://IP地址:端口/api/login/smslogin
  "XDDurl": "",
  ///xddToken
  "XDDToken": "",
  ///登陆预警 0 0 12 * * ?  每天中午十二点 https://www.bejson.com/othertools/cron/ 表达式在线生成网址
  "ExpirationCron": " 0 0 12 * * ?",
  ///个人资产 0 0 10,20 * * ?  早十点晚上八点
  "BeanCron": "0 0 10,20 * * ?",
  // ======================================= WxPusher 通知设置区域 ===========================================
  // 此处填你申请的 appToken. 官方文档：https://wxpusher.zjiecode.com/docs
  // WP_APP_TOKEN 可在管理台查看: https://wxpusher.zjiecode.com/admin/main/app/appToken
  // MainWP_UID 填你自己uid
  ///这里的通知只用于用户登陆 删除 是给你的通知
  "WP_APP_TOKEN": "",
  "MainWP_UID": "",
  // ======================================= WxPusher 通知设置区域 ===========================================
  ///Push Plus官方网站：http": //www.pushplus.plus  只有青龙模式有用
  ///下方填写您的Token，微信扫码登录后一对一推送或一对多推送下面的token，只填" "PUSH_PLUS_TOKEN",
  "PUSH_PLUS_TOKEN": "",
  //下方填写您的一对多推送的 "群组编码" ，（一对多推送下面->您的群组(如无则新建)->群组编码）
  "PUSH_PLUS_USER": "",
  ///青龙配置  注意对接XDD/芝士中括号[]留空 设置为"Config":[]
  "Config": [
    {
      //序号必填从1 开始
      "QLkey": 1,
      //服务器名称
      "QLName": "阿里云",
      //青龙地址
      "QLurl": "http://ip:5700",
      //青龙2,9 OpenApi Client ID
      "QL_CLIENTID": "",
      //青龙2,9 OpenApi Client Secret
      "QL_SECRET": "",
      //CK最大数量
      "QL_CAPACITY": 99,
      ///建议一个青龙一个WxPusher 应用
      "WP_APP_TOKEN": "",
    },
    
    {
      //序号必填从1 开始
      "QLkey": 2,
      //服务器名称
      "QLName": "腾讯云",
      //青龙地址
      "QLurl": "http://ip:5700",
      //青龙2,9 OpenApi Client ID
      "QL_CLIENTID": "",
      //青龙2,9 OpenApi Client Secret
      "QL_SECRET": "",
      //CK最大数量
      "QL_CAPACITY": 99,
      ///建议一个青龙一个WxPusher 应用
      "WP_APP_TOKEN": "",
    }
  ]

}
```

## 特别鸣谢

* [@NNNNolan](https://github.com/NNNNolan)










