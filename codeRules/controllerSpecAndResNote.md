# Controller Spec And Res Note

一切的想了解起因於開 spec

對於回傳的 message 到底該怎麼開 ？  這樣開後端實作會不會有問題 ＝—＝？

才發現真的是 TMDer 完全沒搞清楚訊息 http 的 res 到底是怎麼傳、接到什麼啊 (無數的驚嘆號）

## 目錄

- [問題]

  - [來來來，這些東西你真的搞懂了嗎 ？](https://github.com/TMDer/warehouse/blob/controllerSpec/codeRules/controllerSpecResNote.md#%E4%BE%86%E4%BE%86%E4%BE%86%E9%80%99%E4%BA%9B%E6%9D%B1%E8%A5%BF%E4%BD%A0%E7%9C%9F%E7%9A%84%E6%90%9E%E6%87%82%E4%BA%86%E5%97%8E-)

- [解答]

  - [Controller Return res.XXXX ?](https://github.com/TMDer/warehouse/blob/controllerSpec/codeRules/controllerSpecResNote.md#controller-return-resxxxx-)

  - [Controller Spec](https://github.com/TMDer/warehouse/blob/controllerSpec/codeRules/controllerSpecResNote.md#controller-spec)

***

## 來來來，這些東西你真的搞懂了嗎 ？

```
res.ok result
res.okWithSocket result
res.serverError error
res.serverErrorWithSocket error
res.serverErrorWithSocket ParserService.errorToJson error
```

幾個我們系統中常見的 controller 結尾回傳方式，差異在哪裡你知道嗎 ？


```
request(sails.hooks.http.app)
.post(“/controller/function/")
.send(params).end (error, res)->

  (error == null).should.be.true
  # res.body.should.be ....
  # res.body.should.be ....
```

test spec 這裡的 error 哪裡來 ？

有沒有發現 error 總是 null 呢 ？


#### 如果以上問題能清楚回答，那恭喜你看到這裡就可以了 ～～～～～  YA .

***



***

## Controller Spec

前情提要： `.end (error, res)` 的error 為何總是 null ？

```
  request(sails.hooks.http.app)
  .post(“/controller/function/")
  .send(params)
  .expect(200)
  .end (error, res)->

    (error == null).should.be.true
    # res.body.should.be ....
    # res.body.should.be ....
```
> 沒有用 expect 的話， `(error == null).should.be.true` 都只是像棒球的快樂槍一樣。
> res.body 就等同於 api controller 中最後所傳的 error / data （包含後續對參數的處理變動）。

補充：

- [Testing controllers](http://sailsjs.org/#/documentation/concepts/Testing?q=testing-controllers)為sails 的文件中簡潔的 Demo ，其中透露了使用的套件。

- [supertest](https://github.com/tj/supertest) 為實際使用的套件，可查閱更多 expect 的用法。

***

## 總結

1. 開立 spec 的時候要確認是否需要於前端顯示，直接影響是否使用 Socket。

2. spec 最簡單確認成功與否的方式是：

```
  res.statusCode.should.equal 200 # ok
  res.statusCode.should.equal 500 # error
```
3. 沒有 expect 就不要在對 `.end (error, res)` 中的error下 should 條件。
