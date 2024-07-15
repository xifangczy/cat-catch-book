---
description: 需要猫抓 v2.5.3+
---

# 调用本地程序

<figure><img src="../.gitbook/assets/invoke.svg" alt=""><figcaption><p>调用程序图标</p></figcaption></figure>

设置 - 开启 调用程序。在资源列表页 出现调用按钮 ，点击即可打开你设定的协议。

如果你想要开启的程序没有调用协议 (URL Protocol) 可以使用 [https://github.com/xifangczy/URLProtocol](https://github.com/xifangczy/URLProtocol) 为其注册一个。

以[https://github.com/nilaoda/N\_m3u8DL-RE](https://github.com/nilaoda/N\_m3u8DL-RE) 为例

分别下载以上两个工具，并放置在一起。

打开 URLProtocol 协议名填入 `m3u8dlre`选择调用目标，选择 `N_m3u8DL-RE.exe`

猫抓 - 设置 - 调用程序 - 参数设置

```
m3u8dlre://${url} --save-dir "%USERPROFILE%\Downloads" --del-after-done --save-name "${title}_${now}" --auto-select ${referer|exists:'-H "Referer: *"'}
```

现在已完成所有设置。

想要调用 N\_m3u8DL-RE 点击调用图标皆可。
