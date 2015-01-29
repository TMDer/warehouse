---
layout: post
title:  "Error message 處理方式"
date:   2015-01-15 17:36:07
categories: warehouse work flow
tags: work flow
image: http://www.cypressnorth.com/wp-content/uploads/2012/09/catchAllTheErrors-615x461.png
---

# Error 訊息處理流程

###說明

如果在執行過程產生錯誤，例如要求廣告資料這個孤嗯能，需要提供使用者的ID才能顯示對應的廣告，這時候若未收到使用者的ID便無法繼續執行，所以程式會終止並回傳錯誤訊息。對於處理這個狀況的流程請參考以下建議做法。


### 流程

#####1.使用以下方法產生錯誤訊息

```
  new Error("userId is required")
```

使用這個方式的錯誤，可產生如下提示

```
  debug: Error: userId is required
    at Object.exports.getAllAds (/services/Service.coffee:7:43)
    at module.exports.getAllAds (/Controller.coffee:108:18)
```

如此以來便可以清楚知道問題產生的程式與行數，快速找到問題點

####2.使用套件方式進行轉換 error

  ParserService.errorToJson(error)
透過這個方法可將 error 轉換爲 pmd 常用的格式，如下：

```
  { message: 'userId is required', type: 'danger' }
```

除了有特定的需求，建議盡量使用此格式，前端收到這個格式的錯誤，也可以很方便的顯示在畫面上。

####3.使用 console.error

如果在程式內需要將 error log 出來，可使用 `console.error` 代替 console.log ，這樣的訊息可以更明顯知道是錯誤，也會更容易找到訊息位置。
