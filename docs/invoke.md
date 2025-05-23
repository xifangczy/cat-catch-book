---
description: 需要猫抓 v2.5.3+
---

# 调用本地程序

<figure><img src="../.gitbook/assets/invoke.svg" alt=""><figcaption><p>调用程序图标</p></figcaption></figure>

设置 - 开启 调用程序。在资源列表页 出现调用按钮 ，点击即可打开你设定的协议。

如果你想要开启的程序没有调用协议 (URL Protocol) 可以使用 [https://github.com/xifangczy/URLProtocol](https://github.com/xifangczy/URLProtocol) 为其注册一个。

以[https://github.com/nilaoda/N\_m3u8DL-RE](https://github.com/nilaoda/N_m3u8DL-RE) 为例

分别下载以上两个工具，并放置在一起。

打开 URLProtocol 协议名填入 `m3u8dlre`，选择调用目标 `N_m3u8DL-RE.exe`

猫抓 - 设置 - 调用程序 - 参数设置

```
m3u8dlre:"${url}" --save-dir "%USERPROFILE%\Downloads" --del-after-done --save-name "${title}_${now}" --auto-select ${referer|exists:'-H "Referer: *"'}
```

现在已完成所有设置。

想要调用 N\_m3u8DL-RE 点击调用图标皆可。



## 示例：

### 启用迅雷下载

`thunder://${url|exists:"AA*ZZ"|to:base64}`

### 使用potplayer播放

`potplayer:${url} ${referer|exists:'/referer="*"'}`

## 测试参数

添加参数 `--cat-catch-test` 在调用程序之前会提示即将调用的程序以及参数。

例如 `m3u8dlre:"${url}" --cat-catch-test`

{% hint style="warning" %}
Chrome 自定义 URL Protocol 对于参数中包含 ${url} 的情况，协议名不允许包含双斜杠 "//"
{% endhint %}
