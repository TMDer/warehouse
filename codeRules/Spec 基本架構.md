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
