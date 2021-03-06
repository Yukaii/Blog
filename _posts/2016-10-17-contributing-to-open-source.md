---
layout: post
title: "開源貢獻初體驗"
---

## 第一次的 PR

在兩個月前的暑假，還在努力當個 Rails 工程師的我，為了進行我社產品的重構，想先找個專案練練手。當時 VSCode 開源專案管理的 GithHub 令我好生羨慕，覺得所有的開源專案，如果都能如此有條理的讓人參與貢獻，那該有多好呀。我找了找 Rails 專案，發現之前有在關注的校園專案 [NCTU+](https://plus.nctu.edu.tw/) 當時也在進行改版。

clone 下來看了看，發現 rubocop 上色還挺多的，於是就想也沒想開始玩了起來。煞有介事的開了個 [issue](https://github.com/Yukaii/nctuplus/issues/1)，描述專案多有技術債云云，列出了各式 Todo。首先著手的就是升級 Rails，並且把過時的套件都升級一番。

經過了兩天的折騰後，送出了第一支 [Pull Request][nctuplus]。結果就失敗了 XD。

## 自我愉悅

我想了想，覺得當時的問題有三：

1. PR 太大包
2. 對 Roadmap 不瞭解
3. 沒有測試

最後再附加一個，太自我中心，加了一堆東西卻又沒有附上 Getting Started。

當時我覺得 PR 太大包，其實現在看來也還好，因為「順便」把重複的目錄移除，所以 Git 更改看起來比較多。但是這「順便」就是問題所在了。在跑 GitHub Flow 時，Feature branch 應該單一目的，我雖然 PR 名為「升級 Rails/Ruby/gems」，實際上還是混雜了[多個目標](https://github.com/nctuplus/nctuplus/pull/6#issuecomment-238025911) ，現在看來有點可惜。

對 Product Roadmap 的不瞭解這部分，其實也算該專案的特性。校園團隊的運作方式，大概是[徵才](https://www.facebook.com/nctuplus/posts/1069989203046912) 後大家一起共同成長，所以 Roadmap 既沒有公佈在 GitHub 也沒有在粉專，我這個亂入的傢伙，照著自己意圖亂升級，終究也只是自己的實驗 XD。

最後一點關於測試，其實專案本身就沒啥測試 XD，所以[幫忙 Review 的同學](https://github.com/nctuplus/nctuplus/pull/6#issuecomment-238018884)也有提到，我的 PR 還需要花大把的時間確認能不能運作。這對於當時還在衝刺功能的 NCTU+ Team 來說，確實是個沒有必要的 PR。

總結一下，我既不熟悉 NCTU+ 團隊的運作方式，開出的問題也是假議題（沒必要升級呀），還需要花大把的成本驗證，那這個 PR 就完全是自嗨嘛 :p。

## 於是跑來寫 JavaScript

在大約一個月前~~把自己開除~~轉職回學生之後，除了玩弄下 [SICP](https://mitpress.mit.edu/sicp/) 之外，另一項規劃就是把幾個月前開的坑 [Comics Reader](https://github.com/ComicsReader/reader) 補了補進度。該專案也是 [fork](https://github.com/zeroshine/ComicsScroller) 來的，不過到後來幾乎整個重寫，除了一樣是用 [Material-UI](http://www.material-ui.com/) 界面配色照著改之外，還多了一卡車東西。

起初想要 fork 是因為與其砍掉重練專案，不如發 PR 給原專案，一步步~~入侵~~影響原專案，把它變成自己的形狀。要知道重寫專案成本也是很大的，現在輪子這麼多就別再造了啦，而且原本的插件我也用的很開心。儘管如此，每個人還是都有自己的主觀意識~~工程師的浪漫~~，這世界的輪子才這麼多，我終究還是重造了船 😂。

## 跳入神坑 HackMD - The Realtime Collaborate Markdown Platform

Comics Reader 寫著寫著，對於 JavaScript 這奇妙~~垃圾~~語言的熱情也回來了，也想跳個坑玩一下。常在 [g0v slack](http://join.g0v.today/) 潛水的我注意到 hackfoldr 常常拿來搭配 [HackMD](https://hackmd.io) 使用，一個支援多人即時協作的線上 Markdown 編輯平臺。看了看 [GitHub Repo](https://github.com/hackmdio/hackmd)，發現技術架構剛好與我目前的技能表吻合，那就開始貢獻吧！

## 為 Legacy JavaScript 導入 Webpack

經過幾個開發流程改進的 PR 後([#187][pr187]、[#190][pr190])，我開始[導入 Webpack][pr195] 前端打包器。

此時我對 JavaScript 的理解還停留在 React 這種 SPA 應用上，於是把許多 vendor package 都轉到 npm，然後在進入點引用進來，產生的 JS Bundle 也隨著引用的套件增加而擴大。我後來才理解到把常用的 vendor 放在 CDN 才是好的優化方法，因為瀏覽器會幫你快取，於是我又慢慢地把放到 npm 的套件在 extract 出來，簡直是繞了一大圈啊（汗）。[#195][pr195] 就記錄了這過程。

隨著這份 PR 越來越大包，我也開始覺得緊張，要是合併回去之後，功能通通炸掉怎麽辦？結果確實也是如此，我另外花了 [#202][pr202]、[#205][pr205]、[#206][pr206] 三個 PR 來把大部分的功能修復 😅。

[#195][pr195] 做出改變實在太大了，當時也是邊做邊找資料學習，於是發生了這種繞圈子的意外。好險原作者 jacky 非常 nice 的接受了 PR，也一起確認了各功能是否運作正確 😂。現在上線的版本就是小弟我加料過的，實在緊張刺激 XD。

## 更多的 PR，更多的 Open Source

跳入一個新專案，從 run 起來開始瞭解架構，然後開始惡搞，這就是我最近在幹的事。時常有「挖坑給自己填」之感，這就是_惡搞系工程師_的人蔘啊。

最後再推一下 [HackMD](https://hackmd.io) 這個專案，作者 jacky 在設計上實在加入許多巧思，希望有一天能長成工程師每天用的筆記軟體，繼續填坑讓專案更好！

[nctuplus]: https://github.com/nctuplus/nctuplus/pull/6
[pr187]: https://github.com/hackmdio/hackmd/pull/187
[pr190]: https://github.com/hackmdio/hackmd/pull/190
[pr195]: https://github.com/hackmdio/hackmd/pull/195
[pr202]: https://github.com/hackmdio/hackmd/pull/202
[pr205]: https://github.com/hackmdio/hackmd/pull/205
[pr206]: https://github.com/hackmdio/hackmd/pull/206
