
# Datetime picker

## Module Name
common.dateTimePicker

## 參數說明

### 必填
* ngModel: 回傳的資料類型 String，雙向綁定的 scope 變數

### 選填
* isOpen: 回傳的資料類型 Boolean，date picker 開啟的依據
* maxDate: 傳入的資料類型 String / {{scope}}，許可的最大日期
* minDate: 傳入的資料類型 String / {{scope}}，許可的最小日期
* required: 傳入的資料類型 Boolean，用途是否使用 $vaild
* timeZoneText: 傳入的資料類型 String / {{scope}}，Datetime 最後顯示的文字，例如： Asia Taipei 、台北時間

### Simple Code
```coffeescript
$scope.min = "2015-10-05"
```

```jade
date-time-picker(ng-model="dateTimeModel", min-date="{{min}}" , max-date="2015-10-21")
```


## Todo
* datePickerOptions: 
* dateFormat: 日期元件上顯示的日期格式，目前先固定 `yyyy-MM-dd`
* timeOption: 時間元件設定。傳入 `Objcect`
