---
description: 一个辅助猫抓的在线工具，负责 缓存捕获、在线合并 和 m3u8解析器 合并后转码工作。
---

# 在线ffmpeg

工具链接： [https://ffmpeg.bmmmd.com/](https://ffmpeg.bmmmd.com/)

第一次使用会下载ffmpeg 大约30M 请耐心等待，之后会缓存到浏览器内。

## ffmpeg命令

示例 `ffmpeg -i "av.mp4" -c copy "gv.mp4"`

命令`ffmpeg -codecs` 查看支持的编码\
添加参数 `-nd` 文件处理完不下载文件，直接放入文件区

## 文件区

使用 `加一坨文件` 按钮，或拖动文件到页面上添加文件。

左键点击文件名可以在线预览视频，支持 m3u8 mpd flv 和mp4等各种视频格式。

可拖入字幕文件 在预览视频时点击字幕文件 字幕会载入到播放器上。播放器设置按钮可调 字幕大小以及时间抽偏移。

右键点击文件名 自动在 cmd 光标处填入文件名，方面输入命令。

## 命令列表

<table><thead><tr><th width="152" align="center">命令</th><th width="300" align="center">说明</th><th align="center">示例</th></tr></thead><tbody><tr><td align="center">ffmpeg</td><td align="center">/</td><td align="center">/</td></tr><tr><td align="center">clearFFmpeg</td><td align="center">清理缓存在浏览器的ffmpeg</td><td align="center"></td></tr><tr><td align="center">clear</td><td align="center">清空console</td><td align="center"></td></tr><tr><td align="center">add</td><td align="center">添加网络文件<br>不少网站限制，成功率不高</td><td align="center">add https://bmmmd.com/test.mp4</td></tr><tr><td align="center">down</td><td align="center">下载文区的文件</td><td align="center">down test.mp4</td></tr><tr><td align="center">play</td><td align="center">预览文件<br>参数可以为url</td><td align="center">play test.mp4</td></tr><tr><td align="center">ren</td><td align="center">重命名文件</td><td align="center">ren test.mp4 bmm.mp4</td></tr><tr><td align="center">milk</td><td align="center">赞助</td><td align="center"></td></tr><tr><td align="center">thanks</td><td align="center">赞助感谢名单</td><td align="center"></td></tr><tr><td align="center">help</td><td align="center">帮助</td><td align="center"></td></tr><tr><td align="center">mycat</td><td align="center">🐱</td><td align="center"></td></tr></tbody></table>



{% hint style="info" %}
由于WebAssembly的限制, 在线ffmpeg目前只能处理最大2G的视频。
{% endhint %}
