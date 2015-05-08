# Controller Spec And Res Note

一切的想了解起因於開 spec :

對於回傳的 message 到底該怎麼開 ？  這樣開後端實作會不會有問題 ＝—＝？

才發現真的是 TMDer 完全沒搞清楚訊息 http 的 res 到底是怎麼傳、接到什麼啊 (無數的驚嘆號）

## 目錄

- [問題]

  - [來來來，這些東西你真的搞懂了嗎 ？](https://github.com/TMDer/warehouse/blob/master/codeRules/controllerSpecAndResNote.md#%E4%BE%86%E4%BE%86%E4%BE%86%E9%80%99%E4%BA%9B%E6%9D%B1%E8%A5%BF%E4%BD%A0%E7%9C%9F%E7%9A%84%E6%90%9E%E6%87%82%E4%BA%86%E5%97%8E-)

- [解答]

  - [Controller Return res.XXXX ?](https://github.com/TMDer/warehouse/blob/master/codeRules/controllerSpecAndResNote.md#controller-return-resxxxx-)

  - [Controller Spec](https://github.com/TMDer/warehouse/blob/master/codeRules/controllerSpecAndResNote.md#controller-spec)


## 來來來，這些東西你真的搞懂了嗎 ？

```javascript
res.ok result
res.okWithSocket result
res.serverError error
res.serverErrorWithSocket error
res.serverErrorWithSocket ParserService.errorToJson error
```

- 幾個我們系統中常見的 controller 結尾回傳方式，差異是 ？


```javascript
request(sails.hooks.http.app)
.post(“/controller/function/")
.send(params).end (error, res)->

  (error == null).should.be.true
  # res.body.should.be ....
  # res.body.should.be ....
```

- controller spec 這裡的 error, res.body 哪裡來 ？

- 有沒有發現 error 總是 null 呢 ？

#### 如果以上問題能清楚回答，那恭喜你看到這裡就可以了 ～～～～～  YA .



## Controller Return res.XXXX ?

回顧一下我們常見的回傳方式，想想其中的差異。

```javascript
res.ok result
res.okWithSocket result
res.serverError error
res.serverErrorWithSocket error
res.serverErrorWithSocket ParserService.errorToJson error
```

簡單說：帶有 Socket 的都是 TMDer 我們自己定義的，意義與名稱一樣就是跟 Socket 有關係，

上面的簡單說的看起來就像廢話一樣 ...... 還是直接來看彼此間的結構關係吧。

```javascript
# Sails 定義 / res.status 也是定義的一部分
res.serverError(err, viewOrRedirect, sendSocket = false) ->

  res.status = 500
  # do sth ...

res.ok(data, viewOrRedirect, sendSocket = false) ->

  res.status = 200
  # do sth ...



# TMDer 定義
res.serverErrorWithSocket(err, viewOrRedirect) ->

  @res.serverError(err, viewOrRedirect, true)

res.okWithSocket(data, viewOrRedirect) ->

  @res.ok(data, viewOrRedirect, true)
```

> Sails 與 TMDer 定義的差別真的只有一個：sendSocket。

#### 那傳遞 sendSocket 進去的用意 ？

```javascript
res.serverError(err, viewOrRedirect, sendSocket = false) ->

  if sendSocket
    req.socket.emit "error",
      verb: req.options.action
      model: req.options.controller
      data: err
      locals: locals.error
      id: req.param("id") || “”


res.ok(data, viewOrRedirect, sendSocket = false) ->

  if sails.config.environment isnt "test" && sendSocket
    req.socket.emit "message",
      verb: req.options.action
      model: req.options.controller
      data: data
```
> 會分別在 ok / serverError 中判斷是否丟出 socket.emit


### 小結

如果沒有需要在前端 show 出訊息使用 ` res.ok && res.serverError ` 即可，

反之，需要在前端 show 出訊息則使用 ` res.serverErrorWithSocket &&  res.okWithSocket `。


####  那 ParserService.errorToJson 呢？

ParserService.errorToJson 的 code 如下，與[codeRules/Error訊息處理流程](https://github.com/TMDer/warehouse/blob/master/codeRules/Error%20%E8%A8%8A%E6%81%AF%E8%99%95%E7%90%86%E6%B5%81%E7%A8%8B.md)相關。

```javascript
  ###
    前面定義 error.type 預設為 danger，如果自己有設定就覆蓋。
    最重要的是 return 這段 ， 會將 error 轉成只傳 key 與 陣列內容相符的值 。
    例如：
      error = {msg: 'msg', test: 'test'}
      error 傳進去會回傳  {msg: 'msg', type:'danger'}
      有發現 test 被略掉了嗎 [?!!]
  ###

  return JSON.parse(JSON.stringify(error, ['message', 'type', 'inner', 'msg', "params"], 2))
```

### 小結

沒有特別要回傳其他值時使用 `ParserService.errorToJson` 篩選出需要的訊息即可，

反之，需要回傳其他值時，對於 socket 所需顯示的訊息和格式就需要自行定義。

補充：客製化的 message 則在 `linker/js/common/notice/app.coffee` 調整。



## Controller Spec

前情提要： `.end (error, res)` 的 error 為何總是 null / res.body 是什麼？

```javascript
  request(sails.hooks.http.app)
  .post(“/controller/function/")
  .send(params)
  .expect(200)
  .end (error, res)->

    (error == null).should.be.true
    # res.body.should.be ....
    # res.body.should.be ....
```
> 沒有用 expect 的話 erorr 就只可能是 null ， 而 `(error == null).should.be.true` 就像棒球的快樂槍一樣。

> res.body 等同於 api controller 中最後所傳的 error / data （包含後續對參數的處理變動）。

補充：

- [Testing controllers](http://sailsjs.org/#/documentation/concepts/Testing?q=testing-controllers) 為sails 的文件中簡潔的 Demo ，其中透露了使用的套件。

- [supertest](https://github.com/tj/supertest) 為實際使用的套件，可查閱更多 expect 的用法。



## 總結

- 開立 spec 的時候要確認是否需要於前端顯示，直接影響是否使用 Socket。

- spec 最簡單確認成功與否的方式是：

```javascript
  res.statusCode.should.equal 200 # ok
  res.statusCode.should.equal 500 # error
```
- 沒有 expect 就不要在對 `.end (error, res)` 中的error下 should 條件。
