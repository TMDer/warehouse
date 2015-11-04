
# Datetime picker

## Module Name
common.dateTimePicker

## 參數說明

### 必填
* ngModel: 回傳的資料類型 String (toISOString 格式)，賦予預設值格式限制 Date

```coffeescript
use Javascipt

scope.ngModel = new Date()

use momentjs

scope.ngModel = moment().toDate()
```

### 選填
* isOpen: 回傳的資料類型 Boolean，date picker 開啟的依據
* maxDate: 傳入的資料類型 String / Date (細節可看 simple code)，許可的最大日期
* minDate: 傳入的資料類型 String / Date (細節可看 simple code)，許可的最小日期
* required: 傳入的資料類型 Boolean，用途是否使用 $vaild
* postfix: 傳入的資料類型 String，Datetime 最後顯示的文字，預設是 Asia Taipei 、台北時間
* useKeyboardInput: 傳入的資料類型 Boolean，是否可以用鍵盤輸入日期和時間，預設是 true
* formElementName: 傳入的資料類型 String，自訂 element 的 Form name，預設是 datetimepicker-亂數
* errorMessage: 傳入的資料類型 String，設定 required error 的訊息，預設是 Oops, something error.
* useErrorMsg: 傳入的資料類型 Boolean，是否顯示 reuqired error 的訊息，預設是 false
* changeFn: 傳入的資料類型 fucntion 表達式，ngModel 有更動時觸發

### Simple Code
```coffeescript
$scope.min = "2015-10-05" | moment("2015-10-05").toDate() | "2015-10-14T00:00:00.000Z"
$scope.max = 同 $scope.min
$scope.useKeyboardInput = false
$scope.useChangeFn = ->
  console.log "get change" + Date.now()
```

```jade
date-time-picker(ng-model="dateTimeModel", min-date="min", max-date="max", change-fn="useChangeFn", use-keyboard-input="{{useKeyboardInput}}", use-error-msg="true", error-message="Test error message.")
```


## 未來提供
* datePickerOptions: 
* dateFormat: 日期元件上顯示的日期格式，目前先固定 `yyyy-MM-dd`
* timeOption: 時間元件設定。傳入 `Objcect`
