# Spec 基本架構

```javascript
// 群組
describe "[CRUD] Audience", (done) ->

  // 前置動作：準備所需共用參數、Sino 函式
  before (done) ->
    done()


  // 後續：通常用在註銷 Sino
  after (done) ->
    done()

  // 單元測試： Sino
  it "[C]", (done) ->

    // 定義 input
    parmas = {

    }

    FbService.xxx.xxx parmas, (error, result) ->

      // 用在 Controller 的 Spec
      return done(ParserService.jsonToString(res.body)) if res.statusCode is 500

      // 用在 Service 的 Spec
      return done(ParserService.jsonToString(error)) if error

      done()

```

### 補充、延伸閱讀

- [Controller Spec 錯誤處理.md](https://github.com/TMDer/warehouse/blob/master/codeRules/Controller%20Spec%20%E9%8C%AF%E8%AA%A4%E8%99%95%E7%90%86.md)
- [成功與失敗訊息規格.md](https://github.com/TMDer/warehouse/blob/master/codeRules/%E6%88%90%E5%8A%9F%E8%88%87%E5%A4%B1%E6%95%97%E8%A8%8A%E6%81%AF%E8%A6%8F%E6%A0%BC.md)
