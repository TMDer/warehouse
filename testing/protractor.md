# Protractor usage and installation

 * [protractor](http://angular.github.io/protractor/#/tutorial)

# install

```
npm install -g protractor
webdriver-manager update
npm install -g mocha
```

 * [詳細安裝流程](http://angular.github.io/protractor/#/tutorial)

#prepare

所有的設定都是透過 `protractor.conf.js` ，透過 specs 可以增加 protractor 要執行的檔案，透過這樣子的流程可以順利進行調整。

```
exports.config = {
  framework: "mocha",
  seleniumAddress: "http://0.0.0.0:4444/wd/hub",
  capabilities: {
    browserName: "chrome",
    // (Optional Start) Set if the path of browser is not default install path.
    chromeOptions: {
      binary: "/Applications/Browsers/Google\ Chrome.App/Contents/MacOS/Google\ Chrome",
      args: [],
      extensions: [],
    }
    // (Optional End)
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

### By

可以透過 `By` 物件，找到 angular 已經綁定的物件，或者執行綁定方式等。

```
// find an element using a css selector
By.css('.myclass') 

// find an element with the given id
By.id('myid')

// find an element with a certain ng-model
By.model('name')

// find an element bound to the given variable
By.binding('bindingname')
```

 * [Protractor Locators](http://angular.github.io/protractor/#/locators)
 * [ProtractorBy](http://angular.github.io/protractor/#/api?view=ProtractorBy)


### browser

是指對於瀏覽器上的操作，可以參考底下文件。

 * [Proctractor Browser](http://angular.github.io/protractor/#/api?view=Protractor)

### Element

在頁面上 DOM 物件的操作，取得 DOM 資料。

`element` 可以取得單一物件，例如 #id, 某個物件等。

`element.all` 是取得一連串的物件，例如 li, .class 一連串序列的物件

 * [element.all(locator)](http://angular.github.io/protractor/#/api?view=ElementArrayFinder)
 * [element(locator)](http://angular.github.io/protractor/#/api?view=ElementFinder)



## Warning

在文件上中的 `by` 如果採用 `coffee-script` ，需要改成大寫 `By` ，否則會出現異常錯誤。因為 by 是保留字。

### 已知

目前已知道所有元件得到後，將會包裝為 `promise` 型態，需要使用 `then` 來去讀取資料結果，或者進行下一步驟動作。

有時候會發生 UI 在發生時間點，還沒有進行 render 完成，或者後端沒有回傳資料，可以試著用 

```
browser.waitForAngular()
browser.sleep(1500)
```

目前持續使用 `should` 方式

 * [should spec](http://shouldjs.github.io/)

### 參考資料

 * [Protractor 參考範例](https://github.com/angular/protractor/tree/master/example)
 * [Protractor - 環境設定篇](https://www.facebook.com/notes/paul-li/protractor-%E7%92%B0%E5%A2%83%E8%A8%AD%E5%AE%9A%E7%AF%87/10152948608982211?pnref=lhc)
 * [Protractor - 實戰篇 - Config File](https://www.facebook.com/notes/paul-li/protractor-%E5%AF%A6%E6%88%B0%E7%AF%87-config-file/10152950568012211)
 * [Protractor - 實戰篇 - Page Objects](https://www.facebook.com/notes/paul-li/protractor-%E5%AF%A6%E6%88%B0%E7%AF%87-page-objects/10152952559442211)
 * [Protractor - Enhance 篇 - Trouble Shooting](https://www.facebook.com/notes/10152956325467211/)





