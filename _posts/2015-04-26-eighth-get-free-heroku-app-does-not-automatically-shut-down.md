---
layout: post
title: '第八篇 - 讓免費 Heroku App 不會自動關機'
date: 2015-04-26 15:44
comments: true
categories:
---
免費的 Heroku 開的 App 只要過半小時，就會自動關機。雖然啟動很快，不過體驗就差了。

一般的做法是安裝 [newrelic](https://newrelic.com) 監控，每隔一段時間交流一下，就可維持開機狀態。不過本 ghost 部落格一直設定不起來 newrelic 的 node 套件，只好找了個替代品 [UptimeRobot](https://uptimerobot.com) 來使用。免費的方案可以 monitor 五十個站台，最短 interval 為五分鐘，夠用了。

表現倒是不錯，設定每十五分鐘左右自動 ping 個，就和一般網站一樣啦，皆大歡喜 XD。


![螢幕快照 2015-04-23 上午1.46.37.png](http://user-image.logdown.io/user/1128/blog/1112/post/261901/XxmpYw7CQkESsvFqbM9n_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-04-23%20%E4%B8%8A%E5%8D%881.46.37.png)
