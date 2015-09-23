# pmd_platform 資料夾架構基本介紹
api - 後端 server
  - ∟ controller - Server 介接端口
  - ∟ models - 定義資料格式
  - ∟ policies - controller 接收 request 前的 middleware
  - ∟ responses - controller 回傳 response 前的 middleware
  - ∟ services - 服務層，提供各式 lib
sockets - (無)  
assets - 前端 services
  - ∟ bower - 放置由 bower 下載的第三方套件
  - ∟ images - 圖片
  - ∟ linker - 放置網頁元件
    - ∟ fonts - 字型檔
    - ∟ js - 放置 coffee-script 檔
    - ∟ styles - 放置 .scss/.css 檔
    - ∟ template - 由 angular 控制的動態版型(.jade)  
   
config - Server 各項設定  
queue - (無)  
tasks - grunt 排程設定檔
tests(spec) - 放置測試檔案，基本上對應 api 資料夾底下的檔案；e2e 對應前端操作測試  
views - 網頁靜態版型

# 開發語言

## js
[coffee-script](http://coffeescript.org/) 

## css 
[sass](http://sass-lang.com/) | [compass](http://compass-style.org/)

## template
[jade](http://jade-lang.com/)

# 主要套件介紹

## [angular](https://angularjs.org/)
**前端主要 framework**

## [sails](https://www.npmjs.com/package/sails)
**後端所使用的基本 web-framework**

## [bower](http://bower.io/)
**前端套件管理工具**

## [npm](https://www.npmjs.com/)
**後端套件管理工具**

## [grunt](http://gruntjs.com/)
**排程管理**
設定檔放在 /task 底下
- grunt - 跑開發階段的 asset
- grunt test - 跑 test
- grunt prod - 跑正式機的 asset
- grunt watch - 接 gulp 跑 watch
- gulp watch - 跑 watch
- gulp bootstrap - 跑 server 啟動要做的事情
```
local 檔的載入
run schedule
passport FB的操作相關函式載入
async.waterfall 的部份為建立初始使用者的資料，Task Queue 服務啟動
```

## [gulp](http://gulpjs.com/)
**套件排程管理**  
利用其 streaming 特性負責檔案監控及compiler
 
## [protractor](http://angular.github.io/protractor/)
**前端 UI 測試套件 - [文件參考](https://github.com/TMDer/warehouse/blob/master/testing/protractor.md)**  
負責前端頁面UI 元件操作測試

## [mocha](http://mochajs.org/)
**後端開發測試套件 - [文件參考](https://github.com/TMDer/warehouse/blob/master/tips/test_skill.md)**  
test code 放置於 /test 底下，負責**定義資料傳遞的格式**及各項後端測試 
