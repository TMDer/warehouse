# Controller Spec 錯誤處理

## 前言

當你這樣寫 Spec 的時候有沒有發現 error 總是 null ?

```javascript
request(sails.hooks.http.app)
.post(“/controller/function/")
.send(params).end (error, res)->

  (error == null).should.be.true
  # res.body.should.be ....
  # res.body.should.be ....
```

因為漏掉了 `supertest` 中 `expect` 的用法，
而 `.end` 裡面的 `error` 只會 `catch` 到不符合 `expect` 的內容

## 結論

我們團隊採用不使用 `expect` ，直接判斷 res.stateCode 方式作錯誤處理

```javascript
return done(ParserService.jsonToString(res.body)) if res.statusCode is 500
```

### 補充

- - [supertest](https://github.com/tj/supertest) 為實際使用的套件，可查閱更多 expect 的用法。


