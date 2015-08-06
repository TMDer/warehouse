Proposal/async await

參考說明文章： https://jakearchibald.com/2014/es7-async-functions/

執行測試 command: mocha test/models/await_async.spec.js

基本上就是可以讓你在總是非同步的 javascript 環境裡使用同步的程式處理（like java）

推薦使用情境：

* database 操作
* 簡化 report 處理

缺點：

* 需要用原生的 javascript，也就是副檔名為 *.js

coffeescript 的替代方案：

https://github.com/yortus/asyncawait#asyncawait-101

兩個方式皆可達到同樣的目的，一個是原生未來的 jabvascript feature

一個是保留 coffeescript 的好處，也同樣有 await/async 的特性

其中使用 asyncawait 這套件相容 coffeescript 目前尚未評估，或許可以比較一下兩種方式同樣處理，哪個執行效率比較快

