---
description: N_m3u8DL-CLI  N_m3u8DL-RE 非常优秀的第三方m3u8文件合并下载工具，支持HLS m3u8和DASH mpd
---

# 使用 m3u8dl:// 协议



{% hint style="info" %}
N\_m3u8DL-CLI原作者以停止更新。建议优先使用[N\_m3u8DL-RE](m3u8dl.md#n\_m3u8dl-re)
{% endhint %}

## N\_m3u8DL-CLI

下载N\_m3u8DL-CLI [https://github.com/nilaoda/N\_m3u8DL-CLI/releases](https://github.com/nilaoda/N\_m3u8DL-CLI/releases)

如果你电脑里没有安装ffmpeg 请下载 N\_m3u8DL-CLI\_v3.0.\*\_with\_ffmpeg\_and\_SimpleG.zip

解压后 建议 N\_m3u8DL-CLI\_v3.0.\*.exe 重命名为 m3u8dl.exe 或其他固定名称。否则每次更新版本都需要重新注册协议，以后更新N\_m3u8DL-CLI只需修改文件名替换即可。

使用cmd 运行`m3u8dl.exe --registerUrlProtocol` 注册协议

{% hint style="info" %}
注册完协议后，不要再移动m3u8dl.exe文件的位置。你应该解压到一个固定位置再进行注册。
{% endhint %}

检查是否完成，在浏览器地址栏输入 `m3u8dl://` 回车 是否有如下对话框

<figure><img src="../.gitbook/assets/opm3u8dl.png" alt=""><figcaption></figcaption></figure>

看到此窗口，恭喜你已经完成了`m3u8dl://`协议的注册，之后在猫抓设置， `启用 m3u8dl:// 下载 m3u8 or mpd` 选项选择`N_m3u8DL-CLI`，你可以自定义修改调用参数，点击 `查看参数说明` 按钮查看所有参数列表。

<figure><img src="../.gitbook/assets/2.png" alt=""><figcaption><p>开启调用协议和参数设置</p></figcaption></figure>

如果猫抓嗅探到m3u8或mpd文件的存在，popup页面直接点击文件的下载按钮会直接调用N\_m3u8DL-CLI下载

<figure><img src="../.gitbook/assets/dm3u8.png" alt=""><figcaption></figcaption></figure>

第一次使用会弹出窗口

<figure><img src="../.gitbook/assets/opm3u8dl2.png" alt=""><figcaption></figcaption></figure>

勾选 `始终允许` 下次使用不会再弹出确认窗口。

更多N\_m3u8DL-CLI使用方法，查看官方使用文档 [https://nilaoda.github.io/N\_m3u8DL-CLI/](https://nilaoda.github.io/N\_m3u8DL-CLI/)

## N\_m3u8DL-RE

[https://github.com/nilaoda/N\_m3u8DL-RE](https://github.com/nilaoda/N\_m3u8DL-RE) 是CLI的升级版，原作者全新开发，支持跨平台。但目前不支持m3u8dl:// 协议。需要使用[https://github.com/xifangczy/URLProtocol](https://github.com/xifangczy/URLProtocol) 工具。

下载URLProtocol和N\_m3u8DL-RE 并放置在一起，打开URLProtocol工具，协议名填写 `m3u8dl` 点击选择目标程序按钮，选择`N_m3u8DL-RE.exe` 点击添加。完成了 RE的注册。

{% hint style="info" %}
如果你之前有使用N\_m3u8DL-CLI注册过协议，请使用CLI的--unregisterUrlProtocol 参数卸载。
{% endhint %}

再猫抓设置 `URL Protocol m3u8dl` -> `参数设置` 修改为 N\_m3u8DL-RE 的参数。

示例：

`"${url}" --save-dir "%USERPROFILE%\Downloads\m3u8dl" --save-name "${title}_${now}" ${referer|exists:'-H "Referer:*"'} --del-after-done --no-log`

更多参数查看N\_m3u8DL-RE github页面。

使用和N\_m3u8DL-CLI一致，嗅探到m3u8资源直接点击下载图标即可调用N\_m3u8DL-RE下载该m3u8文件。
