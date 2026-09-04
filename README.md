# 看板（静态版）

全钟瑞舆情监控看板的前端。抓取、翻译、数据库、定时收割全部仍在原来的
Google Apps Script 云端跑，这里只是一个纯静态页面，用跨域 fetch 取数。

## 为什么要有它

2026-09-03 实测：浏览器只要带着 Google 登录 Cookie 访问
`script.google.com/macros/.../exec`，Google 会改写成 `/macros/u/N/...`
并回一个云端硬盘的「很抱歉，目前无法开启这个档案」。三个 Google 账号
（含专案所有者本人）、乃至全新建的空白应用都一样，而匿名访问完全正常。

跨域 fetch 默认不带 Cookie（代码里还显式 `credentials: 'omit'`），
请求以匿名身份到达 Apps Script，正好绕开这个故障。

## 改动方式

不要直接改这里的 `index.html`。改上游那份 `韩笑九全监控-云端/Index.html`，然后：

    python3 生成静态看板.py
    cd 静态看板 && git commit -am 更新 && git push

## 注意

页面里只有一个公开的数据接口地址，没有任何口令或密钥。
推送口令、Gemini key、Bark key 一律不进这个仓库。
