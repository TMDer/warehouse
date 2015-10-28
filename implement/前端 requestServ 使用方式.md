因應後端回傳的資料格式，包裝 $sails.get / $sails.pot 及後續的 success / error callback 處理

#### 後端 okWithSocket 回傳的資料格式 (未經過包裝)
```
{
  ....
}
```

#### 後端 serverErrorWithSocket 回傳的資料格式
```
{
  $error: data
  $id: id
}
```

### requestServ.request(url, param)

#### 參數
- url: 要呼叫的 url
- param: 參數；如有設置，代表 $sails.post，沒設置則是 $sails.get

#### 範例
```
#故意執行會回傳 error 的 post
requestServ.request("/adMgmt/updateAd", {id: 1})
.error((data, id) ->
  console.error "Got Error data", data
  console.error "Got Error id", id
  return
)

#成功取得 objective 例表後 顯示在 jade 頁面
requestServ.request("/adMgmt/campaignObjective")
.success((data) ->
  $scope.campaignObjectives = _.keys(data)
  return
)
.error((data, id) ->
  console.error "Got Error data", data
  console.error "Got Error id", id
  return
)
```
