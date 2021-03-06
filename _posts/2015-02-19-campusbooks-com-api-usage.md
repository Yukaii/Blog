---
layout: post
title: '第六篇 - CampusBooks.com 的 API 使用'
date: 2015-02-19 13:13
comments: true
categories: 
---
好久不見！忙裡偷閒的來篇小記，重理思路再出發。

近一兩個月都在都在處理跟書相關的事，畢竟也算半個書商了，在書籍資料搜尋上，和大家介紹個好站。

## 簡介

[CampusBooks.com](http://www.campusbooks.com/)，據說也是做 SEO 的公司起家，透過此網站，你可以方便的搜尋各類教科書的資料，書名作者 isbn 都基本，還可以直接顯示在各大書店價錢：
<!--more-->


![螢幕快照 2015-02-19 下午9.17.53.png](http://user-image.logdown.io/user/1128/blog/1112/post/255688/ELEkkxHRTyZG68ICOkhQ_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-02-19%20%E4%B8%8B%E5%8D%889.17.53.png)

Google 得知他也是有[開放 api 的](http://www.campusbooks.com/company/api3_documentation.php)，只是要合作才能申請 API key，想想也沒美國時間，就 inspect 了一下他的網站，發現十分工整 rest url：
 
![螢幕快照 2015-02-16 下午2.55.17.png](http://user-image.logdown.io/user/1128/blog/1112/post/255688/iMXYb7oGQmSFYrw7ny9v_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-02-16%20%E4%B8%8B%E5%8D%882.55.17.png)

就直接拿 api key 來用了哈哈。

```shell
SITE_API_KEY = PA52HnTGaTSyizTOq4j1
```

## API

對照了網路上僅存的[第三版 api document](http://www.campusbooks.com/company/api3_documentation.php) 看，先列出幾個基本的，有需要再慢慢找啦：

### 透過 isbn 拿書資料

```shell
GET http://api2.campusbooks.com/13/rest/bookinfo?key=API_KEY_HERE&isbn=xxxxxxx&format=json
```

可以把 json response 打開，否則預設是 xml：

```
&format=json
```

範例結果：

```json
{
    "response": {
        "status": "ok",
        "version": "13",
        "label": {
            "plid": "0",
            "name": "CampusBooks.com",
            "website_id": "0",
            "website_name": "CampusBooks.com"
        },
        "page": {
            "name": "books",
            "f": "search",
            "books": {
                "page": 1,
                "limit": 1,
                "results_returned": 1,
                "total_pages": 1,
                "total_results": 1,
                "book": [
                    {
                        "isbn10": "1111570051",
                        "isbn13": "9781111570057",
                        "author": "",
                        "binding": "Paperback",
                        "edition": "",
                        "image": {
                            "width": 60,
                            "height": 75,
                            "image": "http://ecx.images-amazon.com/images/I/51XzAECQ6xL._SL75_.jpg"
                        },
                        "msrp": 97.62,
                        "pages": "",
                        "publish_date": "",
                        "publisher": "Example Product Manufacturer",
                        "rank": 1603132,
                        "rating": 0,
                        "title": "Brief Applied Calculus. James Stewart, James Stewart, Dan Clegg"
                    }
                ]
            }
        }
    }
}
```

### 拿書價格

把 price field 打開

```shell
GET http://api2.campusbooks.com/13/rest/bookinfo?key=API_KEY_HERE&isbn=xxxxxxx&format=json&f=prices
```

輸出有點長就不貼了。

## 小結

根本沒長到需要寫小結啊（飛踢）

如果沒差舊版的 API 文件太多，其他還有 search / bookprices 可以用，不過我沒有用到就暫時不寫了。

基本上 campusbooks 的書是非常齊全了，他們有從 1998 開始的資料，[OpenLibrary](https://openlibrary.org/) 有些找不到的書，這裡都找的到；順帶一提，OpenLibrary 也有好用的 api，也有 ruby gem，就單本書的資料上會比 campusbooks 更齊。

新年第一篇文，就祝大家新年快樂啦！
