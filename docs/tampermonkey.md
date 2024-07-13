---
description: Tampermonkey 俗称油猴 chrome脚本扩展神器。官方扩展商店对扩展的更新审核非常慢，油猴脚本也能快速编写和更新对特定网站的支持。
---

# 使用油猴脚本给猫抓发送资源

猫抓自带的[深度搜索](other.md#shen-du-sou-suo)虽能满足大部分情况，在对特别保护的网站还是需要一些特殊处理，油猴脚本刚好能弥补猫抓的不足。这里示范如何给猫抓发送数据，以便大家自己写脚本。

通过 `window.postMessage()` 函数可以对猫抓发送一条资源或密钥。

## 发送资源

参数为对象，对象属性如下:

|    属性   |        值(示例)       | 说明                                     |
| :-----: | :----------------: | -------------------------------------- |
|  action | "catCatchAddMedia" | 固定 必须，告诉猫抓添加一条资源                       |
|   url   |         \*         | 资源的地址                                  |
|   href  |    location.href   | 当前页面的网址，让猫抓区分从哪里来的资源。一般为 location.href |
|   ext   |         \*         | 资源的扩展，如果不填写，猫抓会从资源地址分析，可为空             |
|   mime  |         \*         | 资源的mime类型 如: video/mp4，可为空             |
| referer |         \*         | 打开资源所需的referer头属性，可为空                  |

脚本示例

[https://greasyfork.org/zh-CN/scripts/456150/code](https://greasyfork.org/zh-CN/scripts/456150/code)

```javascript
window.postMessage({
    action: "catCatchAddMedia",
    url: "https://github.com/xifangczy/cat-catch",
    href: location.href,
    ext: "test",
    mime: "test/text",
    referer: "https://github.com"
});
```

安装后回到本页面刷新，应该可以看到猫抓会多出来一条资源，这就是从油猴脚本发送的。

也可以用脚本把资源通过GM\_xmlhttpRequest或者ajax/fetch方式下载到内存里，通过new Blob() 和 URL.createObjectURL() 创建一条blob网址发送给猫抓。

```javascript
fetch("https://bmmmd.com/")
.then(response => response.blob())
.then(function (blob) {
    window.postMessage({
        action: "catCatchAddMedia",
        url: window.URL.createObjectURL(blob),
        href: location.href,
        ext: "html",
    });
});
```

## 发送密钥

部分网站的m3u8的密钥不在文件内，需要对网页进行分析得出，可以通过脚本获得密钥发送给猫抓m3u8解析器。详见 [寻找到疑似key](m3u8parse.md#maybekey)

|   属性   |        值(示例)        | 说明                                                                                                                         |
| :----: | :-----------------: | -------------------------------------------------------------------------------------------------------------------------- |
| action |   "catCatchAddKey"  | 固定 必须，告诉猫抓添加一个密钥                                                                                                           |
|   key  |          \*         | 密钥数据，经过base64编码或arrayBuffer类型。                                                                                             |
|  href  |    location.href    | 当前页面的网址，让猫抓区分从哪里来的密钥。一般为 location.href即可                                                                                   |
|   ext  | "base64Key" / "key" | <p>密钥经过base64编码，填入<br>base64Key<br><br>密钥为arrayBuffer类型，填入<br>key</p><p><br><strong>2.3.0 版本之后能自动判断密钥类型，不需要填写</strong></p> |

```javascript
window.postMessage({
    action: "catCatchAddKey",
    key: "aHR0cHM6Ly9ibW1tZC5jb20=",
    href: location.href,
    ext: "base64Key",
});
```

## 在线ffmpeg转格式

需要猫抓2.3.0 以上版本

|   属性   |                      值(示例)                      | 说明                                                         |
| :----: | :---------------------------------------------: | ---------------------------------------------------------- |
| action |                 "catCatchFFmpeg"                | 固定 必须                                                      |
|   use  | <p>"transcode"</p><p>"merge"<br>"onlyAudio"</p> | <p>transcode 格式为 mp4<br>merge 音频视频合并<br>onlyAudio 提取音频</p> |
|  media |                     _Array_                     | <p>媒体文件</p><p>详见 media 对象数组</p>                            |
|  title |                  document.title                 | <p>最后输出的文件名</p><p>可为空</p><p>默认 document.title</p>          |

### media 对象数组

|  属性  |         值         | 说明                                            |
| :--: | :---------------: | --------------------------------------------- |
| data |         \*        | <p>媒体的URL</p><p>可以是blob地址(必须可以正常打开)</p>       |
| type | "video" / "audio" | <p>媒体类型，音频还是视频。</p><p>可为空</p><p>默认"video"</p> |
| name |         \*        | <p>文件名<br>为空自动 "memory"+时间戳 命名<br></p>        |

### 示例 合并音频和视频

```javascript
const media = [];
for (let item of mediaArray) {
    const blob = new Blob(item.buffer, { type: item.mime });
    media.push({data: URL.createObjectURL(blob), type: item.mime});
}
window.postMessage({
    action: "catCatchFFmpeg",
    use: "merge",
    media: media,
    title: document.title
});
```

{% hint style="info" %}
不能连续多次提交，在线ffmpeg不接受多个命令，需等待上一个视频处理完毕。

暂无处理进程回传功能。
{% endhint %}

{% hint style="info" %}
**所有值区分大小写**

**目前接口正在完善中，可能会随时增删改。**
{% endhint %}
