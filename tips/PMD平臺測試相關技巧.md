# PMD平臺測試相關技巧(未完成)

### 緣由
測試常常是在找問題或者是驗證功能完成的必要步驟，但也因爲過程繁瑣，會花費許多細碎的時間，透過一些方式與設定，能夠減少時間花費以提升速度

### 匯入資料到 MySQL
由於某些測試需要反覆的將資料匯入資料庫，單純使用 GUI 工具，需要比較多的操作，若使用指令搭配，可快速的完成這個動作：

```
mysql -uroot -p123456 pmd_platform_test < /Users/Vincent/Desktop/pmd_platform_2015-01-26.sql
```
指令內的各項參數說明如下：

 * -u : 使用者名稱
 * -p : 密碼，若爲空密碼可不帶入
 * pmd_platform_test : 資料庫名稱
 * /Users/Vincent/Desktop/pmd_platform_2015-01-26.sql : 匯入檔案的路徑
 
### 設定 bash_profile
如果你發現上發的指令出現：

```-bash: mysql: command not found```

那是因爲還沒將 MySQL 設定到 PATH 路徑，如果正常執行請跳過這個項目，如果想將 MySQL 增加到系統的 PATH 中，可參考以下做法：

1. 編輯家目錄下 bash_profile 這個檔案 
	
	```vim ~/.bash_profile```
2. 插入以下這行，PATH 後的路徑請以實際 MySQL 的檔案位置爲準 
	
	```export PATH="/usr/local/mysql/bin:$PATH"```
3. 讓系統重新載入這個檔案

	```source ~/.bash_profile```
	
### Sails 的 Error 等級說明
在調整有關 Error 輸出層級的時候，可以先閱讀以下列表，作出更精確的設定：

| Priority | level    |                       Log fns visible                         |
| -------- |:--------:| :------------------------------------------------------------:|
| 0        | silent   |                              N/A                              |
| 1        | error    |                            .error()                           |
| 2        | warn     |                       .warn(), .error()                       |
| 3        | debug    |                  .debug(), .warn(), .error()                  |
| 4        | info     |              .info(), .debug(), .warn(), .error()             |
| 5        | verbose  |        .verbose(), .info(), .debug(), .warn(), .error()       |
| 5        | silly    |    .silly(), .verbose(), .info(), .debug(), .warn(), .error() |


### 篩選執行 test 時的訊息
由於預設在 `test/init/before.coffee` 裏面的 level (Sails.lift:log:level) 是 `debug`，因此可能會輸出與錯誤較無關係的訊息，將這裏的等級改爲 `error`，則只會顯示出 `console.error`方法所產生的訊息，避免不必要的干擾。

### 避免每次執行 test 都會清空資料庫
每次 test 的執行階段，會先行清空資料庫，若有特殊需求，可將 `test/init/before.coffee` 裏面的 migrate (Sails.lift:log:level)預設是 `drop`，設定爲 `safe`，就可以避免清空資料庫的動作。

### 保留 test 後的 Facebook 廣告
在 test 過程所建立的所有檔案，由於只是測試用途，在結束 test 後會呼叫清除程序，將之清除，若在測試完後想保留 Facebook 上的廣告，可在 `test/init/after.coffee` 裏面，`AdCampaignService.cleanAllFbCampaign_danger_only4Test` 之前直接呼叫 `app.lower done` ，可避免 Facebook 上的廣告被清除。

### 將環境設為 production

目前預設在我們本機的`pmd_platform/config/local.coffee`預設環境是 `developement`，但為了在本機測試在正式機的運作流程，就必須將環境變成 `production`，可以將 `environment`的值設定為`production`，另外爲了確保環境與 production 相似，需使用 `grunt prod` 。
```
