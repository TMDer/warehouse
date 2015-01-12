---
layout: post
title:  "開發團隊的 github flow 標準流程"
date:   2015-01-12 12:36:07
categories: jekyll update
---

![](http://s3.amazonaws.com/rapgenius/filepicker%2FEMADv4TRB26cYmN3gyg7_flow.jpg)

## 我們的做法

gitflow 與 code review 太繁瑣，所以無法確保程式品質，因此我們改為 githubflow，並且每個禮拜發布一次，確保開發步奏的循環。

1. 流程改為 github flow
2. 使用 gitlab 的 pull request 來進行
4. 發出 pull request 後會搭配一個觀察者進行 code review
5. 任何人都可以是觀察者
6. 關於程式碼的修改建議一律在 gitlab 上進行
7. 管理人員可以進行 accept request

## git branch 的說明

1. 目前只會保留 develop 跟 master 的分支。
2. **新功能**或是**bug 修正**都從 develop 發起。
3. develop 分支將作為透過 CI 進行上 develop 機測試用。
4. master 一樣做為 production 進行發佈。


## 開發流程

1. 開始一個 feature 或是 bugfix 時，從 develop 切出分支
2. 並且**觀察者**與**開發者**需要整理說明詳細的修改內容，由管理者 accept 時同時填入相關的修改說明。
3. 一旦功能完成，加上上述的使用說明，填寫在 description，發出 pull request
4. 由觀察者確認該功能與程式碼是否有問題，若有問題進行修改。
5. 一旦觀察者確認沒問題再由**管理者**進行 accept

## 時間點說明

1. **禮拜二中午**進行 devlop 環境的 deploy，開始上機測試，若有問題進行 bug 修正
2. **禮拜三中午**開始進行 master 的 deploy，由 master owner 進行最後確認。
3. 完成階段性任務需要進行回報，ticket 將安排優先度，以自願選取有興趣的 task 進行開發。

備註：可能通知方式，再研究


## ticket 的安排，功能切細

一個 ticket 最小**一天**為限，若功能沒辦法在一個禮拜內完成，需要再行切細，必須要是可以進行上線操作的範圍。每次都要有完整的功能可進行測試。


## 退回機制

因為總是還是會有意外的時候，要有退回機制

1. 若有重大錯誤，造成系統 crash 要進行 rebuild
2. 一旦進行 rebulid，hotfix 將在**下次循環**進行 deploy
2. 開始 hotfix 分支從 develop 切出進行
3. 完成後如同開發流程進行 pull request，直到修改完成
4. 進行上機測試
5. 測試沒問題，重新發布


## release note

將由 jenkins 進行 pull 並且打包，因為在「開發流程」中的第三步驟需要詳細說明每一次的更改內容，所以可以自動收集 release note。

## 參考資料

## gitflow
* [Git flow 開發流程](http://ihower.tw/blog/archives/5140)
* [A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)

## githubflow

* [Understanding the GitHub Flow](https://guides.github.com/introduction/flow/index.html)
* [在 GitHub 當中使用的 work flow](http://blog.krdai.info/post/17485259496/github-flow)
* [How GitHub Uses GitHub to Build GitHub](http://zachholman.com/talk/how-github-uses-github-to-build-github/)



## gitflow vs githubflow

* [Git Flow vs Github Flow](http://lucamezzalira.com/2014/03/10/git-flow-vs-github-flow/)


