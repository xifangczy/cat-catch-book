# 常见问题

## 抓不到资源如何做

先尝试[深度搜索](docs/popup-1.md#shen-du-sou-suo)。再尝试[缓存捕捉](docs/popup-1.md#huan-cun-bu-zhuo)，该功能需要等待视频缓冲完毕后才能下载。仍然无法下载，可以尝试最后的[屏幕捕捉](docs/popup-1.md#ping-mu-bu-zhuo)。

如果你遇到只有`缓存捕捉`才能下载资源的网站，请到github提交bug 或 发送邮件。

## 音频和视频分开的

很多网站开始使用音频和视频分离的播放技术，只需要勾选一个音频和一个视频 如果符合条件 会出现 `在线合并`按钮 点击进行合并下载。

{% hint style="info" %}
技术限制，暂时只能合并小于2G的视频，否则只能使用本地工具合并。
{% endhint %}

## 使用缓存捕捉 ffmpeg合并出错

出现 `error reading header` 错误，捕获的文件头部信息缺失，取消ffmpeg合并勾选 下载音频和视频 用第三方工具合并。

## 抓不到YouTube

{% content-ref url="docs/yi-xie-zheng-ze-pi-pei-shi-li.md" %}
[yi-xie-zheng-ze-pi-pei-shi-li.md](docs/yi-xie-zheng-ze-pi-pei-shi-li.md)
{% endcontent-ref %}

## 某鹅通无法下载

尝试使用油猴脚本 [https://greasyfork.org/zh-CN/scripts/461963](https://greasyfork.org/zh-CN/scripts/461963)

脚本会尝试获取m3u8重新拼接正确地址 发送给猫抓。

## 对某个网站常开 深度搜索

安装油猴脚本解决 [https://greasyfork.org/zh-CN/scripts/462831](https://greasyfork.org/zh-CN/scripts/462831)

## m3u8资源合并下载后有声音，但视频花屏

该资源使用了非常规的加密方式，目前暂无办法解决，可以尝试[缓存捕捉](docs/popup-1.md#huan-cun-bu-zhuo)。

## m3u8资源合并下载，打开只显示一张图片 / 碎片资源为png格式

该资源把视频碎片伪装成图片，需要在m3u8解析器勾选 `mp4格式` 该功能会剔除不需要的图片数据或使用第三方工具 N\_m3u8DL-RE 下载。

## m3u8解析器合并下载中页面崩溃

可能下载的文件太大你的内存不够，需勾选 `边下边存` ，勾选该功能后无法使用在线转码功能。

## 在线ffmpeg卡在 **ffmpeg加载中...**

在网页命令框 输入 `clearFFmpeg` 命令 回车 清理ffmpeg 然后刷新页面 重新下载...