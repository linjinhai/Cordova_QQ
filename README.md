# cordova-plugin-qqsdk
[![version](https://img.shields.io/badge/version-0.8.3-blue.svg?style=flat-square)](https://github.com/iVanPan/Cordova_QQ)
[![platform](https://img.shields.io/badge/platform-iOS%2FAndroid-lightgrey.svg?style=flat-square)](https://github.com/iVanPan/Cordova_QQ)
[![GitHub license](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square)](https://github.com/iVanPan/Cordova_QQ/blob/master/LICENSE)
[![Contact](https://img.shields.io/badge/contact-Van-green.svg?style=flat-square)](http://VanPan.me)					

A Cordova wrapper around the Tencent QQ SDK for Android and iOS. Provides access to QQ ssoLogin, QQ Sharing, QQ Zone Sharing etc.. [简体中文](https://github.com/iVanPan/Cordova_QQ/blob/master/README_ZH.md).     
I also write a cordova plugin for WeiboSDK [here](https://github.com/iVanPan/cordova_weibo).                    


## Table of Contents

- [Feature](#feature)
- [Requirements](#requirements)
- [Installation](#installation)
- [Documentation](#documentation)     
  - [Error Code](#error-code)
  - [Support API](#support-api)
  - [Image](#image)  
  - [Usage](#usage)
    - [checkClientInstalled](#checkclientinstalled)
    - [ssoLogin](#ssologin)
    - [logout](#logout)
    - [shareText](#sharetext)
    - [shareImage](#shareimage)
    - [shareNews](#sharenews)
    - [shareAudio](#shareaudio)
    - [getUserInfo](#getuserinfo)
- [About SDK](#about-sdk) 
- [Notes](#notes) 
- [Demo](#demo) 
- [Contributing](#contributing) 
- [License](#license) 

## Feature
1. QQ SSO Login
2. QQ Logout 
3. QQ Share （Text、Image、News、Audio）
4. QQZone Share（Text、Image、News、Audio）
5. QQ Favorites（Text、Image、News、Audio）
6. checkClientInstalled		

## Requirements
- Cordova Version 3.5+ 
- Cordova-Android >=4.0
- Cordova-iOS >=4.0			

##Installation
1. ```cordova plugin add https://github.com/iVanPan/Cordova_QQ.git --variable QQ_APP_ID=YOUR_QQ_APPID``` or ```cordova plugin add cordova-plugin-qqsdk --variable QQ_APP_ID=YOUR_QQ_APPID```                  
2. cordova build          			

##Documentation

###Support API
1. ssoLogin
2. Logout
3. checkClientInstalled
4. Share(see form below)

|      Platform      |   iOS  |   iOS     |     iOS      | Android |  Android  |    Android   |
|        :---:       | :---:  |   :---:   |    :---:     |   :---: |    :---:  |     :---:    |
|      ShareScene    |   QQ   |   QQZone  |  QQ Favorite |    QQ   |   QQZone  |  QQ Favorite |
|      Text        |    √   |     √     |      √       |    ✕    |     √     |      √       |
|      Image         |    √   |     √     |      √       |    √    |     √     |      √       |
|      News        |    √   |     √     |      √       |    √    |     √     |      √       |
|      Audio         |    √   |     √     |      √       |    √    |     √     |      √       |


###Error Code        
When you use qq login,you may get an error code.If you get one, find detail error msg from [here](http://wiki.open.qq.com/wiki/mobile/API%E8%B0%83%E7%94%A8%E8%AF%B4%E6%98%8E#6._.E8.BF.94.E5.9B.9E.E7.A0.81.E8.AF.B4.E6.98.8E%E3%80%82) please.

###Image
 This plugin support three Image types:
  1. Network URL
  2. Base64
  3. Absolute file path         
 
###Usage
#####checkClientInstalled
  ```js
  QQSDK.checkClientInstalled(function () {
      alert('client is installed');
  }, function () {
      // if installed QQ Client version is not supported sso,also will get this error
      alert('client is not installed');
  });

  ```
#####ssoLogin
  ```js
  QQSDK.ssoLogin(function (args) {
      alert("token is " + args.access_token);
      alert("userid is " +args.userid);
      alert("expires_time is "+ new Date(parseInt(args.expires_time)) + " TimeStamp is " +args.expires_time);
  }, function (failReason) {
      alert(failReason);
  });

  ```
#####logout
  ```js
  QQSDK.logout(function () {
      alert('logout success');
  }, function (failReason) {
      alert(failReason);
  });

  ```
#####shareText
  ```js
  var args = {};
  args.scene = QQSDK.Scene.QQ;//QQSDK.Scene.QQZone,QQSDK.Scene.Favorite
  args.text = "这个是Cordova QQ分享文字";
  QQSDK.shareText(function () {
      alert('shareText success');
  }, function (failReason) {
      alert(failReason);
  },args);

  ```
#####shareImage
  ```js
  var args = {};
  args.scene = QQSDK.Scene.QQ;//QQSDK.Scene.QQZone,QQSDK.Scene.Favorite
  args.title = "这个是Cordova QQ图片分享的标题";
  args.description = "这个是Cordova QQ图片分享的描述";
  args.image = "https://cordova.apache.org/static/img/cordova_bot.png";
  QQSDK.shareImage(function () {
      alert('shareImage success');
  }, function (failReason) {
      alert(failReason);
  },args); 

  ```
#####shareNews
  ```js
  var args = {};
  args.scene = QQSDK.Scene.QQ;//QQSDK.Scene.QQZone,QQSDK.Scene.Favorite
  args.url = "https://cordova.apache.org/";
  args.title = "这个是Cordova QQ新闻分享的标题";
  args.description = "这个是Cordova QQ新闻分享的描述";
  args.image = "https://cordova.apache.org/static/img/cordova_bot.png";
  QQSDK.shareNews(function () {
      alert('shareNews success');
  }, function (failReason) {
      alert(failReason);
  },args);

  ```
#####shareAudio
  ```js
  var args = {};
  args.scene = QQSDK.Scene.QQ;//QQSDK.Scene.QQZone,QQSDK.Scene.Favorite
  args.url = "https://y.qq.com/portal/song/001OyHbk2MSIi4.html";
  args.title = "十年";
  args.description = "陈奕迅";
  args.image = "https://y.gtimg.cn/music/photo_new/T001R300x300M000003Nz2So3XXYek.jpg";
  args.flashUrl = "http://stream20.qqmusic.qq.com/30577158.mp3";
  QQSDK.shareAudio(function () {
      alert('shareAudio success');
  }, function (failReason) {
      alert(failReason);
  },args);
  ```
#####getUserInfo
```js
  var url = "https://graph.qq.com/user/get_user_info?access_token=" + accessToken + "&oauth_consumer_key=" + QQ_APP_ID + "&openid=" + userId;
  http.get(url)
```

## About SDK 
This plugin use 3.1.2 version sdk for Android,3.1.3 version sdk for iOS. You can download lastest version sdk [here](http://wiki.connect.qq.com/sdk%E4%B8%8B%E8%BD%BD)              

##Notes             
1. This plugin is required cordova-android version >=4.0,so using cordova  5.0.0 or higher is recommended
2. This plugin should be used after the deviceready event has been fired!!!       
3. ~~If cordova version  <5.1.1,when two cordova plugins are modifying “*-Info.plist” CFBundleURLTypes, only the first added plugin is getting the changes applied.so after installing plugin,please check the URLTypes in your Xcode project.You can find this issue [here](https://issues.apache.org/jira/browse/CB-8007)~~ Update:This Bug is fixed in last cordova version(5.1.1) 
4. For Android: make sure your signature is correct !!!
5. long share URL and large image shoud be avoid.       

##Demo     
1. install this plugin
2. backup www folder in your cordova project
3. replace www by example_www
4. install cordova-plugin-camera
5. cordova build & test     
<div style="text-align:center"><img src="https://github.com/iVanPan/Cordova_QQ/blob/master/ScreenShot.png?raw=true" alt="example" style="width:300px"></div>                                


## Contributing
Feel free to contribute                 

## License

**cordova-plugin-qqsdk** is released under the **MIT** license. See [LICENSE](https://github.com/iVanPan/Cordova_QQ/blob/master/LICENSE) file for more information.




