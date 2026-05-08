# 设置

## **扩展和类型匹配规则**

浏览器接收到文件时判断

![抓取后缀](../.gitbook/assets/f.png)

![抓取类型](../.gitbook/assets/g.png)

抓取类型，也称为[mime](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Guides/MIME_types)扩展类型，部分网站不提供正确的文件后缀，需使用mime扩展类型判断文件，子类型支持通配符 `*` 。

扩展版本 2.6.8 开始过滤大小 允许使用关系运算符。

支持 `> >= < <= = !=` 以及范围表达。容量单位支持 `B KB MB GB`\
例如:

`>= 200KB` 大于等于200KB的资源

`< 1GB` 小于1GB的资源

`!=500KB` 不等于500KB的资源

`500-1024 MB` 500MB到1G范围的资源

## **正则匹配**

浏览器准备打开这个URL之前就对这个URL进行正则匹配。所以优先级最高。

![正则匹配](../.gitbook/assets/6cb98d0e-c99d-4968-abb2-afbf40e98043.png)

**扩展** 猫抓无法知道正则匹配的资源类型，需要指定一个扩展名，留空会尝试截取网址的后缀名，由于许多网址没有后缀所以可能最终无法知晓类型，无法在popup页面显示相应的解析器入口或播放图标。

**屏蔽资源** 可以屏蔽某些不想抓取的资源。

{% hint style="info" %}
正则匹配效率低下，尽量减少正则的使用，避免资源占用过多。
{% endhint %}

## 屏蔽网址

在部分网址上不需要扩展，可以设置网址，支持通配符，例如 `https://x.com/*`

开启 设置为白名单 选项，列表更改为白名单，只有该名单内的网址扩展才会正常工作。

## 复制选项

方便使用第三方工具，点击popup页面复制按钮，直接复制你想要的字符串。

![复制选项](../.gitbook/assets/93d0482c-78d6-4c73-880a-7a175a0c6ccc.png)

### URL Protocol m3u8dl

<figure><img src="../.gitbook/assets/2.png" alt=""><figcaption></figcaption></figure>

具体查看[m3u8dl.md](m3u8dl.md "mention")

## 替换标签

<figure><img src="../.gitbook/assets/replace.png" alt=""><figcaption></figcaption></figure>

### 自定义保存文件名

需打开 **其他设置** 里 `使用自定义文件名保存文件` 选项。可以创建目录 例`${title}/${fullFileName}` 最后储存在 以 title 创建的文件夹内。



## 标签系统 / 替换关键词(2.3.1+) <a href="#keywords" id="keywords"></a>

用于 复制 、数据发送、URL Protocol m3u8dl、调用程序、替换标签 等 使用的关键词替换。标签区分大小写。

详细查看 [tag.md](tag.md "mention")

## 其他设置

![其他设置](../.gitbook/assets/a8c637f4-65b5-4453-89b2-45eb349979b0.png)

### 始终不启用猫抓下载器

下载文件时，检测到资源服务器拒绝下载会重新打开猫抓下载器携带referer参数重新下载文件。如果你使用第三方下载软件打开该选项禁止猫抓下载器被调用。

### 使用本地播放器调用协议打开视频预览 <a href="#player-protocol" id="player-protocol"></a>

部分本地播放器有调用协议，如PotPlayer 有 `potplayer://` 猫抓就能使用该协议直接调用potplayer去播放抓取的资源。

支持替换标签

右侧 `调用协议模板` 下拉菜单有常用的播放器协议。只有部分安卓浏览器支持`intent:`协议调用，所以手机用户更建议使用 `系统分享` 模式。

不使用调用协议 删除清空即可。

{% hint style="info" %}
系统分享模式对浏览器版本有需求。

具体查看[https://caniuse.com/mdn-api\_navigator\_share](https://caniuse.com/mdn-api_navigator_share)
{% endhint %}

### **m3u8dl://协议调用**

具体查看教程[m3u8dl.md](m3u8dl.md "mention")

### 刷新、跳转到新页面 清空当前标签抓取的数据

分为 不清空 正常清理 频繁清理。

其中 频繁清理 比较敏感，比如视频网站，点击观看下一个视频时会先清空。

正常清理 严格按照 是否用户主动刷新，主动点击新链接到新页面，以上动作才会触发清空。

频繁清理可能会导致部分网站在嗅探到资源后立刻被清理，遇到嗅探不到资源的网站，请先尝试清理模式改为 正常 或者 不清理。

### 嵌套在线ffmpeg

在使用在线ffmpeg过程中，各种复杂原因数据传输失败，在线ffmpeg没收到数据，可以打开这个选项，使用嵌套的在线ffmpeg解决。

## 发送数据 <a href="#send" id="send"></a>

能够自定义发送数据到第三方地址上，请求体 确保为JOSN格式

`${action}`为特殊标签, 表示不同数据类型, 如果是捕获数据替换为 `catch` 字符串, 如果是密钥数据 会被替换为 `addKey` 字符串。

如果`${action}` 是`catch` ${data} 则为 文件对象转为JSON格式内容

如果`${action}` 是`addKey` ${data} 则为 密钥base64字符串

示例: `{"action": "${action}", "data": ${data}, "tabId": "${tabId}"}`

```json
// {"action": "${action}", "data": ${data}, "tabId": "${tabId}"}
{
    action: "catch",
    data: {
        name: "文件名",
        url: "资源地址",
        size: "资源大小"
        requestHeaders: {
            referer: "也可能不存在",
            origin: "也可能不存在",
            cookie: "也可能不存在"
        }
        ...: "其他"
    },
    tabId: "数据来源的tab ID"
}

// JSON 接受到疑似密钥
{
    action: "addKey",
    data: "base64数据",
    tabId: "数据来源的tab ID"
}
```

{% hint style="info" %}
数据发送功能测试中，不同版本JSON结构会有差异。
{% endhint %}
