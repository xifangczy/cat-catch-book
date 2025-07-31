---
description: 用于 复制 、数据发送、URL Protocol m3u8dl、调用程序、替换标签 等 使用的关键词替换。标签区分大小写。
---

# 标签系统 / 替换关键词

## 替换标签

<table data-full-width="false"><thead><tr><th width="211">标签</th><th width="275">说明</th><th>结果 示例</th></tr></thead><tbody><tr><td><strong>${url}</strong></td><td>资源地址</td><td>https://bmmmd.com/test.mp4</td></tr><tr><td><strong>${referer}</strong></td><td>资源请求头<br>如果资源不存在referer不输出内容, 建议配合exists函数</td><td>https://bmmmd.com/</td></tr><tr><td><strong>${initiator}</strong></td><td>类似于永远有值的 ${referer}<br>如果资源不存在referer则使用来源网址域名或当前页面网址。</td><td>https://bmmmd.com</td></tr><tr><td><strong>${webUrl}</strong></td><td>资源播放页面地址</td><td>https://bmmmd.com/test.html</td></tr><tr><td><strong>${title}</strong></td><td>资源播放页面的标题</td><td>测试视频</td></tr><tr><td><strong>${fullFileName}</strong></td><td>完整文件名</td><td>test.mp4</td></tr><tr><td><strong>${fileName}</strong></td><td>文件名，不包含扩展</td><td>test</td></tr><tr><td><strong>${ext}</strong></td><td>扩展名，不包含"."</td><td>mp4</td></tr><tr><td><strong>${userAgent}</strong></td><td>User Agent 自定义在设置 - 替换标签 修改</td><td>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36</td></tr><tr><td><strong>${cookie}</strong></td><td>资源所需的cookie <strong>有可能为空</strong><br>格式为 key=value;key=value;<br>需要猫抓 2.3.8版本</td><td>key=value;key2=value2;</td></tr><tr><td><strong>${mobileUserAgent}</strong></td><td>同样也是模拟手机时用的User Agent</td><td></td></tr><tr><td><p>${year}</p><p>${month}</p><p>${date}<br>${hours}<br>${minutes}<br>${seconds}</p></td><td>时间相关，年/月/日/时/分/秒</td><td>*</td></tr><tr><td>${day}</td><td>星期几(英文)</td><td>Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday</td></tr><tr><td><strong>${now}</strong></td><td>unix 时间戳</td><td>1672329448871</td></tr><tr><td><strong>${fullDate}</strong></td><td>日期</td><td>2020-12-28</td></tr><tr><td><strong>${time}</strong></td><td>时间</td><td>21'30'55</td></tr><tr><td>${shareApi}</td><td>系统分享API 只允许在 <a data-mention href="tag.md#player-protocol">#player-protocol</a></td><td></td></tr><tr><td>${range}</td><td>生成范围标签 只允许在m3u8解析器入口使用 详情查看 <a data-mention href="m3u8parse.md#https-bmmmd.com-usd-range-1-5-.ts">#https-bmmmd.com-usd-range-1-5-.ts</a></td><td></td></tr></tbody></table>

## 函数支持

以上列表标粗的标签可以使用函数

<table><thead><tr><th width="123.33333333333331">函数</th><th width="188">说明</th><th>示例</th></tr></thead><tbody><tr><td>slice</td><td>字符截取</td><td><p><code>${title|slice:0,5}</code><br>提取标题前5个字符</p><p><br><code>${title|slice:-10}</code><br>提取标题末尾10个字符<br><br>参数设定来自 js语言 slice 函数</p></td></tr><tr><td>replace</td><td>字符替换</td><td><code>${fullFileName|replace:".m3u8",".mp4"}</code><br>文件名中的".m3u8"字符替换成".mp4"<br><br><code>${title|replace:"网站",""}</code><br>删除标题中 网址 一词<br><br>参数设定来自 js语言 replace 函数</td></tr><tr><td>replaceAll</td><td>字符替换</td><td>同上<br>replace 只替换一次。replaceAll 多次替换。<br><br><code>${fullDate|replaceAll:"-","/"}</code><br>2020/12/28<br>把日期的分隔符换成 "/"</td></tr><tr><td>regexp</td><td>正则提取</td><td><code>${url|regexp:"(https?://[^?]*)"}</code><br>资源地址，提取不包含参数的地址</td></tr><tr><td>exists</td><td><p>如果存在则输出</p><p>反之输出第二个参数，没有第二参数，不输出任何内容。</p></td><td><p><code>${referer|exists:'--headers "Referer:*"'}</code><br>如果存在referer 则输出 --headers "Referer:*"<br>*号最终会被替换成referer本身。</p><p><em>建议填写在m3u8DL参数内，如果存在referer向m3u8DL传递<code>--headers</code>参数，如果没有则不传递。</em></p><p><br><code>${fullFileName|exists:"*","${title}"}</code><br>如果有文件名输出自己，没有文件名输出网页标题。</p></td></tr><tr><td>to</td><td><p>字符串转换<br>base64<br>urlEncode</p><p>urlDecode<br>lowerCase<br>upperCase<br>filter</p></td><td><p><code>${title|to:base64}</code></p><p>5rWL6K+V6KeG6aKR</p><p>base64编码<br><br><code>${url|to:urlEncode}</code><br>https%3A%2F%2Fbmmmd.com%2Ftest.m3u8<br>url编码<br><br><code>${url|to:lowerCase}</code> 英文字母转小写<br><code>${url|to:upperCase}</code> 英文字母转大写<br><br><code>${url|to:filter}</code>  无法作为文件名的字符替换为HTML 字符实体</p></td></tr><tr><td>filter</td><td>过滤/替换 无法作为文件名的字符</td><td><code>${url|filter:"_"}</code> 把不能作为文件名的字符 替换为 下划线<br>被替换的字符 <code>&#x3C; > : " | ? * ~</code></td></tr></tbody></table>

支持链式调用，例如&#x20;

`${url|regexp:"(https?://[^?]*)"|replace:"http://","https://"|to:base64}`

将从左到右依次对url进行，提取 替换 转换base64操作。
