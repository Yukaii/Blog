---
published: false
layout: post
title: 來推廣一下 Alfred 好了
---
## 日常刷存在感開始

三個月沒有發新的文章了。雖然斷斷續續累積了不少內容在 Evernote 和 GitHub 票上，但就是懶的整理成文章發表。看看我，連新年新希望都懶的刷了。若是非要給去年來個總結，大致就是「運氣真好，幹得不錯」吧（結果還是總結了嘛，總結還是比開支票輕鬆的）

今天要來推廣一下 macOS 下的神器 Alfred，其實我也用了快四年了，只是去年才還債 Powerpack（？）

[Alfred][alfred] 除了能**快速啟動/切換**應用程式外，還能編寫自己的 workflow 腳本，來達成匯率轉換、[翻譯][alfred-translate]、即時顯示資訊等等。雖然理論上能透過 API 做到各種應用，但 UI 限制就擺在那，有些功能你硬要用 Alfred workflow 做就顯得彆鈕 😆。

好了，這樣就推廣完畢了（逃）。接下來寫點我自己對 Alfred 做的修改和套件：

[alfred]: https://www.alfredapp.com/
[alfred-translate]: https://github.com/zetavg/alfred-google-translate-workflow

## 自製的 macOS 風格主題 (macOS-styled alfred theme)

![mac-os-styled-alfred-theme](https://i.imgur.com/zg25hcK.png)

[下載連結][alfred-theme-dl]

[alfred-theme-dl]: https://www.alfredapp.com/extras/theme/R20A5tyTVc/

### 特色

- macOS 標準藍色，參見 [Apple Human Interface Guidelines 的色彩部分][1]
- ~~深度微調的背景糢糊和黑色~~ 其實就是肉眼觀測法
- 還不錯的 scrollbar

[1]: https://developer.apple.com/macos/human-interface-guidelines/visual-design/color/

好啦廢話一堆，受限於 Alfred 的 API，主題能調整的也就那些了，反正不要太突兀，和系統風格差不多就好了。~~像我就只會抄 Spotlight~~

BTW，Alfred 分享網址出來的預覽圖實在有點醜啊，應該很久沒更新了吧 XD

## 自己來寫 Powerpack

使用 JS Hero [sindresorhus][2] 大大的 [alfy][3] 套件，就可以輕鬆的用 Node.js 來寫 Alfred workflow，各種 `npm` 套件隨你用，還可以利用 `npm` 來發佈、安裝 workflow。

像我就寫了個內部分機表速查的小工具，誰打電話來找麻煩，要接還是不接，一按就知道！❤️ （被揍）

![alfred-contacts](https://i.imgur.com/9YzPPwQ.png)

> Skitch 馬賽克馬的好糾結

[2]: https://github.com/sindresorhus
[3]: https://github.com/sindresorhus/alfy

## Awesome alfred

反正 [Awesome][awesome] 系列都這麼多年了，什麼不會就讀一讀吧 XD

[awesome]: https://github.com/derimagia/awesome-alfred-workflows
