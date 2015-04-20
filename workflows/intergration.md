#intergration 整合測試流程

當每次 sprint 即將結束之前，都會把所有的資料進行整合，開始佈署到伺服器上，進行新版本程式的轉移。

因為每次有太多不同的意外出現，這邊將所有共同發生的常見例外組織起來，讓大家在開發的時候可以更為全面，建議每次整合測試都將本表單印出，進行勾選確認。

## 整合流程項目說明，

### db 有無加欄位 (dev / preview 環境中)

有的話要發在 important，讓大家知道這次資料庫有進行更新，確定本機更新後正常。

當資料確認完成後，就將 Database schema 更新到 dev / preview 環境中。

### merge develop 確認有無衝突

功能完成後需要發 pull request 到 develop (branch) 確認運作是否正常

### 佈署 preview 版本

將程式發佈 preview / dev 環境中，相關人員進行人工測試檢測項目功能，以及畫面問題，同步進行功能 preview 看看有沒有問題。

### merge 後功能確認

基本上應該沒有問題，本地端簡單的啟動 server 確認是否正常。
需要運行 function test, API test, UI test 以及 3rd party API test

### prodcution 資料確認

若有異動資料庫，請將 produciton 現行資料取回 (or dump) 並且上更新 sql 語法運行確認相關功能是否正常。
這邊因為是正式資料所以不運行 test。

PS. 相關 test 在上一步驟確認

### prodcution 程式更新 / 發佈

將 develop 程式整併到 Master，透過 Jenkins 自動透過上述完整測試流程之後，通過方能進行版本發佈更新到 production。

以上步驟完成後，再請相關人員進行手工測試，進行本次程式測試。

# 整合流程確認表，

- [ ] 確認 db 有無加欄位 (dev / preview 環境中)
  - [ ] 更新欄位資訊發佈於 Important
  - [ ] 確定本機更新 db 後正常
  - [ ] 更新 db 資訊到 dev / preview
- [ ] merge develop 確認有無衝突
- [ ] 佈署 preview 版本
- [ ] merge 後功能確認
  - [ ] function / spec test
  - [ ] API test
  - [ ] 3rd party API test
  - [ ] UI test
- [ ] prodcution 資料確認
  - dump / backup production db
  - 更新 production db
- [ ] production 程式更新 / 發佈
  - [ ] develop merge 到 master
  - [ ] Test by Jenkins
  - [ ] deployed

### 整合測試負責人

###______________________________________


### 整合日期

###______________________________________



