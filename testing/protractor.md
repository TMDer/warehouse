# Protractor usage and installation

 * [protractor](http://angular.github.io/protractor/#/tutorial)

# install

```
npm install -g protractor
webdriver-manager update
```

#prepare

所有的設定都是透過 `protractor.conf.js` ，透過 specs 可以增加 protractor 要執行的檔案，透過這樣子的流程可以順利進行調整。

```
exports.config = {
  framework: "mocha",
  seleniumAddress: "http://0.0.0.0:4444/wd/hub",
  capabilities: {
    browserName: "chrome"
  },
  specs: ["test/**/*.js"],
  baseUrl: 'http://localhost:' + (process.env.HTTP_PORT || '1337'),
  ignoreSynchronization: true
};
```


## start


前端測試會啟動 selenium driver server, `http://localhost:4444/wd/hub` ，這邊會採用 `chrome` 進行測試核心運行。

```
# start web server
webdriver-manager start

```

同時間我們也要啟動 web server 讓前端可以進行測試。

```
npm start
```

## usage

透過底下設定檔案開始進行測試。會透過平台開始

```
protractor protractor.conf.js
```

## 使用說明


### browser

是指對於瀏覽器上的操作，可以參考底下文件。

 * [Proctractor Browser](http://angular.github.io/protractor/#/api?view=Protractor)

### Element

在頁面上 DOM 物件的操作，取得 DOM 資料。

`element` 可以取得單一物件，例如 #id, 某個物件等。

`element.all` 是取得一連串的物件，例如 li, .class 一連串序列的物件

 * [element.all(locator)](http://angular.github.io/protractor/#/api?view=ElementArrayFinder)
 * [element(locator)](http://angular.github.io/protractor/#/api?view=ElementFinder)

### By

可以透過 `By` 物件，找到 angular 已經綁定的物件，或者執行綁定方式等。

 * [ProtractorBy](http://angular.github.io/protractor/#/api?view=ProtractorBy)


## Warning

在文件上中的 `by` 如果採用 `coffee-script` ，需要改成大寫 `By` ，否則會出現異常錯誤。因為 by 是保留字。

有時候會發生 UI 在發生時間點，還沒有進行 render 完成，或者後端沒有回傳資料，可以試著用 

```
browser.waitForAngular()
browser.sleep(1500)
```

### 參考資料

 * [Protractor 參考範例](https://github.com/angular/protractor/tree/master/example)





