# Test 測試方式

如果在除錯的時候，檢測 test 很多時候都會採用到以下的模式，採用 mocha 進行測試, should 作為驗證，

```
describe("test for myself", function(done) {
  it("check data is true", function (done) {
  
  // execute and get obj result
  (obj === null).should.be.true
  console.log(obj);
  return done();

  }); 
})
```

這樣子做其實不會有太多問題，但是會讓這個 `console.log` 顯得有點多餘。

為了省卻這麼多的步驟，因此架構上會改成架構如下，

```
describe("test for myself", function(done) {
  it("check data is true", function (done) {
  
  // execute and get obj result
  if (obj === null).should.not.be.true
    return done(obj);

  }); 
})
```

這樣的方式就可以省卻 `console.log` ，真正顯示資料會是在錯誤的時候，當執行正確就會繼續執行 test pass。
