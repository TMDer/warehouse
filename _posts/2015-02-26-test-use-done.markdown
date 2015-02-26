---
layout: post
title:  "程式碼錯誤檢測方式，減少使用不必要的 console.log"
date:   2015-02-26 12:36:07
categories: warehouse work flow
tags: work flow
image: http://www.metaltoad.com/sites/default/files/testing-darth-vader-300x240.jpg
---

目前團隊內測試架構採用 mocha 進行測試, should 作為驗證，在團隊不斷的累積下，目前測試資料已經超越 1000 多筆資訊，因此留下來的 log 數量都會非常的驚人，而且發現很多資料是沒有必要的。因此我們做了一些改善及建議。

大部分在一開始寫 `test` 開始除錯的時候，檢測 test 很多時候都會採用到以下的模式，

```
describe("test for myself", function(done) {
  it("check data is true", function (done) {
  
  // execute and get obj result
  (obj === null).should.be.true
  console.log(obj);
  return done();

  }); 
})
```

這樣子做其實不會有太多問題，資料也都會正確顯示出來，但是就是因為 `console.log` 隨著時間飛逝，資料也隨之增加，但是會讓這個 `console.log` 顯得有點多餘。

為了省卻這麼多的步驟，因此架構上會改成架構如下，

```
describe("test for myself", function(done) {
  it("check data is true", function (done) {
  
  // execute and get obj result
  if (obj === null).should.not.be.true
    return done(obj);

  }); 
})
```

這樣的方式就可以省卻 `console.log` ，真正顯示資料會是在錯誤的時候，當執行正確就會繼續執行 test pass。

## 結論

一開始的時候需要檢測資料的確是有需要的，不過在資料越來越多的狀況下，如果能精簡資訊，只提供必要的資料時，就會變成一個學問。

目前團隊已經進行了許多不同的測試及資料整合，透過以上的經驗，會開始增進自己的程式碼結構，透過上面的編寫方式，的確也讓資料量減少許多，使的真正的錯誤可以顯示出來，節省掉大量的儲存空間，及人工檢測時間。
