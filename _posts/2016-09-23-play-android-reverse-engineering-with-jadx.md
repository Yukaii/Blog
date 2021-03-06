---
layout: post
title: "用 jadx 來玩玩 Android 逆向工程"
---

## 你幹嘛沒事要來逆向工程啦

~~就是因為沒事啊~~。呃不對，其實以前就有聽說過 Android 逆向工具很成熟，不過自從換 iPhone 後就沒怎麼關注 Android 發展了，一直沒機會玩到。

昨天下午剛好就在臉書刷到一款課表 App，就簡稱為 「X 社小工具」好了，可以幫你匯入學校的課表，支援多個學校。看了看截圖，感覺是在手機端輸入校務系統登入帳密達成，X 社小工具會幫你抓下來，只是不知道後面 API 怎麽跑（誰知道）。秉持著好奇的心，就讓我來逆向看看吧 XDDD。

## 沒手機也要下載 APK

直接把 APK 的 bundle id 貼到 [androidapk](https://androidappsapk.co/apkdownloader/) 這個網站就可以下載了，bundle id 長得像 `com.facebook.katana`。

## jadx 反編譯工具

![jadx](https://camo.githubusercontent.com/bd3c0ea851c23c4535e43590a86c940a0786faa6/687474703a2f2f736b796c6f742e6769746875622e696f2f6a6164782f6a6164782d6775692e706e67)

借一下[官方][jadx]的截圖，[jadx][jadx] 可以直接開啟 apk 檔，把 decompile 過的原始碼顯示出來；除了 gui 界面也有 command line 工具可以讓你直接轉存 source。

載下來解壓縮後有四個檔案：

```bash
.
├── jadx
├── jadx-gui
├── jadx-gui.bat
└── jadx.bat
```

`cd` 進去目錄後執行 `./jadx-gui`，GUI 界面開啟照著操作，選擇你要解開的 apk 就會顯示 Java code 了，也可以選擇轉存，用你喜歡的 Editor 或 IDE 開起來。

## 讀讀讀讀讀 code

不像當初 [Pokemon Go 被逆向](https://applidium.com/en/news/unbundling_pokemon_go/) 一樣，竟然連個混淆都沒做，X 社小工具解出來的原始碼裡，變數都被換成英文字母 abcde，不過想想我的目的就是拿到 API，就直接搜尋 `http://`、`https://` 網址開頭的字串~~

### Retrofit

然後就找到了這段：

```java
public Retrofit a(as asVar) {
    return new Builder().baseUrl("https://容我隱藏一下.appspot.com/").addConverterFactory(GsonConverterFactory.create()).addCallAdapterFactory(RxJavaCallAdapterFactory.create()).callbackExecutor(AsyncTask.THREAD_POOL_EXECUTOR).client(asVar).build();
}
```

看網址 Server 還是用 Google App Engine 架的 XD

[Retrofit](https://square.github.io/retrofit/) 是 Android 用的 HTTP 客戶端，雖然沒用過，不過對於 Retrofit 用 Decorator 標記各個 Endpoint 的寫法印象很深，Retrofit 首頁的範例就這樣寫：

```java
public interface GitHubService {
  @GET("users/{user}/repos")
  Call<List<Repo>> listRepos(@Path("user") String user);
}
```

接下來只要再找出各式 Decorator 就行啦！

### API Endpoints

```java
public interface a {
    ...
    ...

    @GET("schools")
    h<Map<String, j>> a();

    @POST("login")
    h<f> a(@Body e eVar);

    @GET("users/{uid}/schedule")
    h<g> a(@Path("uid") String str, @Header("Authorization") String str2);

    ...
    ...
}
```

上面是其中一段程式碼，看起來主要的 API Endpoint 都在這了。

接下來可以用 `curl` 或 [Postman](https://www.getpostman.com/) 來試打 API，從 GET 的 Endpoint 開始，照著 Login 流程做。不過打 schedule API 的時候卻發現重大問題：

> 我的課表根本就沒課啊！！

所以 `schedule` 只好當做不知道怎麽解了哈哈哈😂

### RxJava

題外話一下，X 社小工具也用了當紅的 Reactive Programming，反編譯後的原始碼就看到一堆短短的 presenter 檔案。

### 其實要拿 API 也不需要反編譯

可以用 [Wireshark](https://www.wireshark.org/) 之類的封包擷取工具撈一下，不過還是看原始碼直接啦😅

## 感想

看來 ProGuard 一類的混淆工具還是有用的，變數、類別都被換掉，腦內理解搜尋速度至少慢了十倍啊，還沒辦法直接 Go to Definition...

本來想寫個免責聲明，不過敏感資訊都已經藏起來了，應該還好吧 XD 這篇只是個人純粹玩工具、讀讀 code 的心得而已，不要追殺我啊 😂😂😂

[jadx]: https://github.com/skylot/jadx
