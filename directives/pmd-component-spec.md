

# Basic Component

## ::basicButton  
#### Module Name
commonApp.basicBtn

#### 參數說明
* draft: 指定常用的按鈕樣式，會自動套入預設的 color 和 text
* color: 按鈕顏色
* text: 顯示文字
* fa: 按鈕圖示的 class
 
#### draft
prev / next / cancel / submit / icon-create / icon-delete / icon-copy / icon-edit / icon-sync

#### color
gray(default) / green / purple

#### fa
https://fortawesome.github.io/Font-Awesome/icons/

#### disabled
true / false
   
#### 使用範例
    
```
basic-btn(draft="prev")
basic-btn(draft="next")
basic-btn(draft="cancel")
basic-btn(draft="submit")
basic-btn(draft="icon-create")
basic-btn(draft="icon-delete")
basic-btn(draft="icon-copy")
basic-btn(draft="icon-edit")
basic-btn(draft="icon-sync")
basic-btn(color="purple", text="Home", fa="fa-home fa-fw")
basic-btn(color="purple", text="Home", fa="fa-home fa-fw", ng-disabled="true")
basic-btn(color="green", fa="fa-refresh")
basic-btn(color="green", fa="fa-refresh", ng-disabled="true")
```
   
  
## ::basicCheckbox
#### Module Name
common.basicCheckbox


#### 參數說明
* checkboxData(required): 元件要顯示的內容陣列
* checkboxModel(required): 元件被選取後要綁定的 scope 變數
* checkboxChange: 元件變更選取項目時要觸發的 function
* checkboxName: 元件的群組名稱
* checkboxObject: 可以使用元件提供的 function 的物件(checkboxName 需設置)

#### checkboxData
{ text:"要顯示的文字", value: "點選後的值", checked: true/false, disabled: true/false }

#### checkboxObj 提供的 function
* selectAll() : 全選/反全選 有相同 checkboxName 的元件
* reverseAll()： 反選取 有相同 checkboxName 的元件

#### 使用範例

```
ifAllChecked = ->
  return $scope.foodList.length is $scope.foodParamList.length

ifEnableSelectAllIcon = ->
  unless ifAllChecked()
    $scope.selectAllFoodsParam.checked = false
    return
  $scope.selectAllFoodsParam.checked = true

$scope.selectAllFoodsParam = {text: "Check All"}

$scope.reverseFoodsParam = {text: "Reverse All"}

$scope.foodParamList = [
  {text: "Noodle", value: "noodle", checked: true}
  {text: "Rice", value: "rice"}
  {text: "Hamburger", value: "hamburger"}
  {text: "Chicken", value: "chicken", checked: true, disabled: true}
  {text: "Beef", value: "beef", disabled: true}
]

$scope.foodList = []

$scope.selectAllCheckbox = ->
  $scope.foodParamList.selectAll()
  return

$scope.reverseAllCheckbox = ->
  $scope.foodParamList.reverseAll()
  ifEnableSelectAllIcon()
  return

$scope.changeCheckbox = (item) ->
  console.log "checked item=", item
  ifEnableSelectAllIcon()
  return
```
```
div
  | Food:
  div
    span(style="margin-left:10px")
      basic-checkbox#selectAllFoods(checkbox-data="selectAllFoodsParam" checkbox-change="selectAllCheckbox()")

    span(style="margin-left:10px")
      basic-checkbox#selectAllFoods(checkbox-data="reverseFoodsParam" checkbox-change="reverseAllCheckbox()")

  div
    span(ng-repeat="foodCheckboxData in foodParamList" style="margin-left:10px")
      basic-checkbox(checkbox-object="foodParamList" checkbox-name="foods"
      checkbox-data="foodCheckboxData" checkbox-model="foodList"
      checkbox-change="changeCheckbox(item)")
  div
  | {{foodList}}
``` 
   
   
## ::basicInput
#### Module Name
commonApp.basicInput

#### 參數說明
* noticeDom: 想要設為 [notice 訊息 DOM] 的搜尋(.find())條件

#### noticeDom 參數
* noticeColor: "red" / "green" 要顯示的訊息顏色，預設為無(黑色)
   
#### 使用範例

```
form(name="fridayForm" novalidate=)
  basic-input(type="text" name="name" placeholder="Please insert your name"
  ng-model="basicInput.name" notice-dom="#notice1, #notice2"
  ng-minlength="3" required)

  #notice1(notice-color ="red" ng-show="fridayForm.name.$error.required") Can not be empty
  #notice2(notice-color ="green" ng-show="fridayForm.name.$error.minlength") Min-length must >= 3

  basic-input(type="text" name="phone" placeholder="Please insert your phone"
  ng-model="basicInput.phone" notice-dom="#notice3, #notice4"
  ng-minlength="7" required)

  #notice3 This is normal notice
  #notice4(notice-color ="green" ng-show="fridayForm.phone.$error.minlength") Min-length must >= 7

  basic-input(tag-name="textarea" name="address" placeholder="Please insert your address"
  width="68%" height="100px"
  ng-model="basicInput.address")

| {{basicInput}}
```   
   
   
## ::basicRadio
#### Module Name
commonApp.basicRadio

#### 參數說明
* radioData(required): 元件要顯示的內容陣列
* name(required): 元件名稱(要設定才能讓 radio 裡的項目綁定為一組)
* radioModel: 元件被選取後要綁定的 scope 變數
* radioChange: 元件變更選取項目時要觸發的 function
* radioDisabled: 將此元件變更爲不可選取狀態

#### radioData
{ text:"要顯示的文字", value: "點選後的值" }

#### radioDisabled
true / false

#### 使用範例
```
$scope.changeRadio = (item) ->
  console.log "selected item=", item
  console.log "$scope.target=", $scope.target
  return
  
$scope.sexRadioDataList = [
  {text: "Man", value: "man"},
  {text: "Woman", value: "woman"},
]

$scope.ageRadioDataList = [
  {text: "<12", value: "12"},
  {text: "<20", value: "19"},
  {text: ">=20", value: "20"}
]

$scope.petRadioDataList = [
  {text: "Dog", value: "dog"},
  {text: "Cat", value: "cat", disabled: true},
]

$scope.target = {
  sex: "man"
  age: "12"
  pet: ""
}

$scope.disabledAll = true
```
```
div
  | Sex:
  div(ng-repeat="sexRadioData in sexRadioDataList")
    basic-radio(name="sex", radio-data="sexRadioData", radio-change="changeRadio(item)", radio-model="target.sex")
  | Age:
    div(ng-repeat="ageRadioData in ageRadioDataList")
    basic-radio(name="age", radio-data="ageRadioData", radio-model="target.age")
  | Pet:
    div(ng-repeat="petRadioData in petRadioDataList")
    basic-radio(name="pet", radio-data="petRadioData", radio-change="changeRadio(item)", radio-model="target.pet", radio-disabled="petRadioData.disabled")
```

## ::basicDropdown  
#### Module Name
commonApp.basicDropdown


#### 參數說明
* items(required): Dropdown Items，項目不可重複 (Array)  
	`[1, 3, , 443, "test"]`
`[{A: a1, B: b1, C: c1}, {A: a2, B: b2}, {A: a3, C: c3}]`
* item-key: 配合 items 使用，如果內部資料是 Object，則需要調入要查找的 key。
	例如要找尋`[{A: a1, B: b1, C: c1}, {A: a2, B: b2}, {A: a3, C: c3}]` 中的 `A`則傳入`A`

* defalut-position: 預設顯示的項目 (Int)，預設值是`0`
* selected-position(required): 目前選擇項目的位置 (Array 中的第幾項, Int)
* status: dropdown 的狀態(default, disabled, locked)，預設值是`default`
	* default:  
	![default](./directive-images/dropdown-default.png)  
	* disabled:  
	![default](./directive-images/dropdown-disabled.png)  
	* locked:  
	![default](./directive-images/dropdown-locked.png)  
* pmd-change: 使用者點選後觸發的動作 (Function)
* disabled: 是否要停用這個物件(Boolean)，預設值是`false`


#### 使用方式
`basic-dropdown(item-key="key" status="default" items="trafficValueArgs", defalut-position="0", selected-position="trafficTypePosition" pmd-change="selectedWebsiteTraffic(trafficArgs[trafficTypePosition], trafficTypePosition)")`


## ::pmdCheckbox
#### Module Name
common.pmdCheckbox


#### 參數說明
* checkboxData(required): 元件要顯示的物件
* ngModel(required): 元件被選取後要綁定的變數
* type: 形狀 round / square
* pmdChange: 元件變更選取項目時要觸發的方法
* disableAll: 將此元件變更爲不可選取狀態

#### 使用方式

```
$scope.checkboxData = [
      {text: "Today", value: "Today"},
      {text: "Yesterday", value: "Yesterday", checked:true},
      {text: "Tomorrow", value: "Tomorrow", disabled:true}
    ]
pmd-checkbox(checkbox-data="checkboxData", ng-model="seletecCheckbox", pmd-change="changCheckbox()")  
pmd-checkbox(checkbox-data="checkboxData", ng-model="seletecCheckbox", pmd-change="changCheckbox()", disable-all="true")
```
