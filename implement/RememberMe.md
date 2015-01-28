# Remember Me 實作

## 概述

- 使用套件 [passport-remember-me](https://github.com/jaredhanson/passport-remember-me)

- 修改相關檔案


  - [config/bootstrap.coffee](https://github.com/TMDer/warehouse/blob/master/implement/RememberMe.md#-configbootstrapcoffee)  - 套件的基本配置

  - [config/http.coffee](https://github.com/TMDer/warehouse/blob/master/implement/RememberMe.md#-confighttpcoffee) - 自定義的 middleware

  - [api/services/UserService.coffee](https://github.com/TMDer/warehouse/blob/master/implement/RememberMe.md#-apiservicesuserservicecoffee) - 對 db 的處理

  - [api/controllers/AuthController.coffee](https://github.com/TMDer/warehouse/blob/master/implement/RememberMe.md#-apicontrollersauthcontrollercoffee) - login成功時的處理



## 流程
![RemeberMeFlow](http://i.imgur.com/8VDr8dl.png)

- cookie 用來存驗證的token
- session 用來存放後端系統所需的資料（例如：使用者、adAccount)

> 流程圖為 [Mak](https://github.com/malikid) 繪製


## 實作

#### :: config/bootstrap.coffee

使用套件並作基本的配置。

```
  RememberMeStrategy = require('passport-remember-me').Strategy;

  passport.use new RememberMeStrategy(
    (token, cb) ->
      UserService.consumeSessionToken token, (err, user) ->
        cb err, user
    , UserService.issueSessionToken
  )

```


#### :: config/http.coffee

自定義的 middleware，用來處理自動 login 後系統所需的 session 存放。


```
passport = require("passport")
module.exports.http =
  customMiddleware: (app) ->
    app.use passport.initialize()
    app.use passport.session()
    app.use passport.authenticate('remember-me')
    app.use sails.config.http.isRememberMeUserToSessition

  isRememberMeUserToSessition: (req, res, next) ->
    isAuthenticated = UserService.isAuthenticated(req)
    user = UserService.getCurrentUser(req)

    if isAuthenticated is undefined and !!req.user
      searchFactor = {id: req.user.id}
      UserService.getLoginUser searchFactor, (err, user) ->
        return next() if err

        req.session.user = user
        req.session.authenticated = req.isAuthenticated()
        req.session.isAdmin = UserService.isAdmin(req)

        # session 沒有 adAccount 時設置 session
        unless req.session.adAccount
          req.session.adAccount = user.adAccounts[0]
        return next()

    else return next()

```

#### :: api/services/UserService.coffee
處理與 token 有關的資料庫存取。

```

# Issue a session token for a userz
exports.issueSessionToken = (user, cb) ->

  User.findOne(user.id).exec (err, newUser) ->

    unless user.sessionTokens
      newUser.sessionTokens = []

  #產生一個新的 token 存入 db
    token = uuid.v4()
    newUser.sessionTokens.push token
    newUser.save (err) ->

      # return 的 token 會在套件的機制下存入 session 中
      # 第一次登入的時候需要自己手動存入 session
      return cb(err, token)


# Consume a user's session token
exports.consumeSessionToken = (token, cb) ->

  User.findOne({sessionTokens: {contains: token}}, (err,user) ->
    return cb(err) if err
    return cb(null, false) unless user

    # 將使用過的 token 從 db 中刪除確保 token 只有一次使用性
    if user.sessionTokens
      user.sessionTokens.forEach (sessionToken, index) ->
        if sessionToken is token
          delete user.sessionTokens[index]

    # 清除陣列中 falsy 的值，例如：false, null, 0
    user.sessionTokens = _.compact(user.sessionTokens);

    # 儲存
    user.save (err) ->
      return cb err, user
  )


```


#### :: api/controllers/AuthController.coffee
第一次記住我且登入成功時，需要產生一個 token 放入 db 與 session 中。

```
req.logIn user, (error) ->

return next(error)  if error
if req.body.remember_me

  UserService.issueSessionToken user, (err, token) ->
    return next(err)  if err
    res.cookie('remember_me', token, { path: '/', httpOnly: true, maxAge: 604800000 });
    successLoginAction(req, res, user)

else
  successLoginAction(req, res, user)

```
