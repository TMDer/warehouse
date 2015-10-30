#### 選單： [basicButton](#basicbutton) | [basicCheckbox](#basiccheckbox) | [basicDropdown](#basicdropdown) | [basicInput](#basicinput) | [basicRadio](#basicradio)

# Basic Component

## ::basicButton  
#### Module Name
commonApp.basicBtn

#### 參數說明
* draft: 指定常用的按鈕樣式，會自動套入預設的 color 和 texts
* color: 按鈕顏色
* text: 顯示文字
* fa: 按鈕圖示的 class
* btnObject: 讓 basicBtn 設置支援 function 用的物件
 
#### draft
prev / next / cancel / submit / icon-create / icon-delete / icon-copy / icon-edit / icon-sync

#### - color
gray(default) / green / purple

#### - fa
https://fortawesome.github.io/Font-Awesome/icons/

#### - btnObject 支援的 function
  **toggleSpin: 旋轉/停止按鈕裡面的圖案**   
   
#### 使用範例
```
$scope.syncBtnObject = {}
$scope.synBtnClick = ->
  $scope.syncBtnObject.toggleSpin()
  return
```
```
basic-btn(draft="prev")
basic-btn(draft="next")
basic-btn(draft="cancel")
basic-btn(draft="submit")
basic-btn(draft="icon-create")
basic-btn(draft="icon-delete")
basic-btn(draft="icon-copy")
basic-btn(draft="icon-edit")
basic-btn(draft="icon-sync" btn-object="syncBtnObject" ng-click="synBtnClick()") # 設置 btn-object
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

#### - checkboxData 格式
{ text:"要顯示的文字", value: "點選後的值", checked: true/false, disabled: true/false }

#### - checkboxObj 提供的 function
  **isSelectedCheckbox(values, force) 檢查元件是否有被選取**   
    values: checkbox 對應的 value， 可為字串或由字串組成的陣列，null 代表全部   
    force: true / false，當 checkbox 為 disabled 時，是否執行   
   
  **isEnabledCheckbox(values) 檢查元件是否可被點選**   
    values: checkbox 對應的 value，可為字串或由字串組成的陣列，null 代表全部   

  **selectCheckbox(values, force) 選取元件**   
    values: checkbox 對應的 value，可為字串或由字串組成的陣列，null 代表全部   
    force: true / false，當 checkbox 為 disabled 時，是否執行   
    
  **unSelectCheckbox(values, force) 反選取元件**   
    values: checkbox 對應的 value，可為字串或由字串組成的陣列，null 代表全部   
    force: true / false，當 checkbox 為 disabled 時，是否執行   
   
  **selectAllCheckbox(force) : 全選/反全選 有相同 checkboxName 的元件**   
    force: true / false，當 checkbox 為 disabled 時，是否執行   

  **clickCheckbox(values, force) 點擊元件**   
    values: checkbox 對應的 value，可為字串或由字串組成的陣列，null 代表全部   
    force: true / false，當 checkbox 為 disabled 時，是否執行   
    
  **enableCheckbox(values) 將元件設成 enable**   
    values: checkbox 對應的 value，可為字串或由字串組成的陣列，null 代表全部   
    
  **disableCheckbox(values) 將元件設成 disable**   
    values: checkbox 對應的 value，可為字串或由字串組成的陣列，null 代表全部   
   
#### 使用範例

```
ifSwitchIcon = ->
  if $scope.foodParamList.isSelectedCheckbox()
    $scope.selectAllFoodsParam.checked = true
  else
    $scope.selectAllFoodsParam.checked = false

  if $scope.foodParamList.isSelectedCheckbox(null, true)
    $scope.selectAllFoodsForceParam.checked = true
  else
    $scope.selectAllFoodsForceParam.checked = false

  if $scope.foodParamList.isEnabledCheckbox()
    $scope.disableFoodsParam.checked = true
  else
    $scope.disableFoodsParam.checked = false

  if $scope.foodParamList.isEnabledCheckbox("rice")
    $scope.disableRiceParam.checked = true
  else
    $scope.disableRiceParam.checked = false

  if $scope.foodParamList.isEnabledCheckbox(["hamburger", "chicken"])
    $scope.disableHCParam.checked = true
  else
    $scope.disableHCParam.checked = false

$scope.selectAllFoodsParam = {text: "Check All"}
$scope.selectAllFoodsForceParam = {text: "Force Check All"}
$scope.reverseFoodsParam = {text: "Reverse All"}
$scope.reverseFoodsForceParam = {text: "Force Reverse All"}
$scope.disableFoodsParam = {text: "Enable All"}
$scope.disableRiceParam = {text: "Enable Rice", checked: true}
$scope.disableHCParam = {text: "Enable Hamburger/Chicken"}
$scope.foodParamList = [
  {text: "Noodle", value: "noodle"}
  {text: "Rice", value: "rice", checked: true}
  {text: "Hamburger", value: "hamburger", checked: true}
  {text: "Chicken", value: "chicken", checked: true, disabled: true}
  {text: "Beef", value: "beef", disabled: true}
]
$scope.foodList = []

$scope.selectAllCheckbox = (data, event) ->
  $scope.foodParamList.selectAllCheckbox()
  ifSwitchIcon()
  return

$scope.selectAllCheckboxForce = (data, event) ->
  $scope.foodParamList.selectAllCheckbox(true)
  ifSwitchIcon()
  return

$scope.reverseAllCheckbox = (data, event) ->
  $scope.foodParamList.clickCheckbox(null)
  ifSwitchIcon()
  return

$scope.reverseAllCheckboxForce = (data, event) ->
  $scope.foodParamList.clickCheckbox(null, true)
  ifSwitchIcon()
  return

$scope.switchEnableCheckboxAll = (data, event) ->
  if $scope.foodParamList.isEnabledCheckbox()
    $scope.foodParamList.disableCheckbox()
  else
    $scope.foodParamList.enableCheckbox()
  ifSwitchIcon()
  return

$scope.switchEnableCheckboxRice = (data, event) ->
  if $scope.foodParamList.isEnabledCheckbox("rice")
    $scope.foodParamList.disableCheckbox("rice")
  else
    $scope.foodParamList.enableCheckbox("rice")
  ifSwitchIcon()
  return

$scope.switchEnableCheckboxHC = (data, event) ->
  values = ["hamburger", "chicken"]
  if $scope.foodParamList.isEnabledCheckbox(values)
    $scope.foodParamList.disableCheckbox(values)
  else
    $scope.foodParamList.enableCheckbox(values)
  ifSwitchIcon()
  return

$scope.changeCheckbox = (item) ->
  console.log "checked item=", item
  ifSwitchIcon()
  return
return
```
```
div
  | Food:
  div
    span(style="margin-left:10px")
      basic-checkbox(checkbox-data="selectAllFoodsParam" checkbox-change="selectAllCheckbox")
    span(style="margin-left:10px")
      basic-checkbox(checkbox-data="selectAllFoodsForceParam" checkbox-change="selectAllCheckboxForce")
    span(style="margin-left:10px")
      basic-checkbox(checkbox-data="reverseFoodsParam" checkbox-change="reverseAllCheckbox")
    span(style="margin-left:10px")
      basic-checkbox(checkbox-data="reverseFoodsForceParam" checkbox-change="reverseAllCheckboxForce")
    span(style="margin-left:10px")
      basic-checkbox(checkbox-data="disableFoodsParam" checkbox-change="switchEnableCheckboxAll")
    span(style="margin-left:10px")
      basic-checkbox(checkbox-data="disableRiceParam" checkbox-change="switchEnableCheckboxRice")
    span(style="margin-left:10px")
      basic-checkbox(checkbox-data="disableHCParam" checkbox-change="switchEnableCheckboxHC")

  div
    span(ng-repeat="foodCheckboxData in foodParamList" style="margin-left:10px")
      basic-checkbox(checkbox-object="foodParamList" checkbox-name="foods"
      checkbox-data="foodCheckboxData" checkbox-model="foodList"
      checkbox-change="changeCheckbox")
  div
  | amount: {{foodParamList.selectedAmount}}
  | value: {{foodList}}
``` 
   
   
## ::basicDropdown  
#### Module Name
commonApp.basicDropdown
   
#### 參數說明
* items(required): 下拉選單的選項，可為一般陣列或有 key 值的物件陣列
```
[1, 2, 3, 4]
[{A: a1, B: b1, C: c1}, {A: a2, B: b2}, {A: a3, C: c3}]
```
* item-key: 配合 items 使用，如果內部資料是 Object，則需要調入要查找的 key
```
[{A: a1, B: b1, C: c1}, {A: a2, B: b2}, {A: a3, C: c3}]
item-key = A 時 => [a1, a2, a3]
item-key = B 時 => [b1, b2]
item-key = C 時 => [c1, c3]
```
* dropdown-change: 使用者點選後觸發的動作 (Function)
* dropdown-model: 下拉選單綁定的值
* dropdown-disabled: 是否要停用這個物件(Boolean)，預設值是`false`
* title: 當沒有綁定 dropdown-model 或 其實為空的時候，所要顯示的文字
* width: 下拉選單寬度 

#### dropdown-change 可以取得的 callback 參數
- value: 選取的值
- index: 選取的 inedx
- event: event 事件

#### 使用範例
```
$scope.dropdownParam = {
  items1: [1, 3, 443, "aaa"]
  items2: [
    {A: "a1", B: "b1", C: "c1"}
    {A: "a2", B: "b2", C: "c2"}
    {A: "a3", C: "Cccccccccc cccccccccccccccccc"}
  ]
  dropdownDisabled: false
  selectedItem: {
    a: "aaa"
    b: ""
    c: "c2"
  }
  itemKey1: "B"
  itemKey2: "C"
}
$scope.dropdownDisabled = false

$scope.changeDropdown = (value, index, event) ->
  $scope.dropdownDisabled = true
  return

$scope.changeDropdown2 = ->
  # return false 可以阻止 basicDropdown 把值設到 ng-model(如果有的話)
  console.log "dropdownParam.selectedItem.a=", $scope.dropdownParam.selectedItem.a
  console.log "dropdownParam.selectedItem.b=", $scope.dropdownParam.selectedItem.b
  console.log "dropdownParam.selectedItem.c=", $scope.dropdownParam.selectedItem.c
  $scope.dropdownParam.selectedItem.c = "c1"
  return false
```
```
div
  | 選擇之後 disabled
  div
    basic-dropdown(title="Please select a number" items="dropdownParam.items1"
    dropdown-change="changeDropdown"
    dropdown-model="dropdownParam.selectedItem.a" dropdown-disabled="dropdownDisabled")
    | selectedItem.a= {{dropdownParam.selectedItem.a}}
div
  | dropdown-change 回傳 false 的下拉選單,並改變 $scope. selectedItem3 = “c1”
  div
    basic-dropdown(items="dropdownParam.items2" item-key="dropdownParam.itemKey1"
    dropdown-change="changeDropdown2" dropdown-model="dropdownParam.selectedItem.b")
    | selectedItem.b= {{dropdownParam.selectedItem.b}}
div
  | normal
  div
    basic-dropdown(items="dropdownParam.items2" item-key="dropdownParam.itemKey2"
    dropdown-model="dropdownParam.selectedItem.c")
    | selectedItem.c= {{dropdownParam.selectedItem.c}}
```
   
   
## ::basicInput
#### Module Name
commonApp.basicInput

#### 參數說明
- width: 指定 input 寬度，預設 100%
- height: 指定 input 高度，預設 30px

#### 在 basic-input 裡面支援的內容
- .input-icon： 要放在 input 裡面的圖案
- .input-notice： 要放在 input 底下的訊息
- 

#### .input-icon 參數(因應 .fa 的圖案位置需要調整):
- iconWidth: 設定 width
- iconSize: 設定 font-size
- iconTop: 設定 padding-top
- iconLeft: 設定 padding-left

   
#### 使用範例

```
form(name="demoForm" novalidate)
  # input 佔滿一行
  .form-group(basic-input)
    # 圖示
    i.input-icon.fa.fa-fw.fa-phone(icon-width="30px" icon-size="20px" icon-top="1px" icon-left="10px")

    input(type="text" name="phone" placeholder="Please insert your phone"
    ng-model="basicInput.phone" ng-minlength="7" required)

    # 提示訊息
    .input-notice This is normal notice
    .input-notice(notice-color ="green" ng-show="demoForm.phone.$error.minlength") Min-length must >= 7

  # 指定 input 寬度，讓 input 併排
  .form-group
    span(basic-input width="120px")
      | this is disable 1:
      input(type="text" name="love" placeholder="This is disabled" disabled)
    span(basic-input width="150px" style="margin-left:10px")
      | this is disable 2:
      input(type="text" name="hate" placeholder="This is disabled")

  basic-btn(draft="submit" ng-click="getInputValue()" ng-disabled="demoForm.$invalid")
```   
   
   
## ::basicRadio
#### Module Name
commonApp.basicRadio

#### 參數說明
- radioData(required): 元件要顯示的內容陣列
- radioName(required): 元件名稱(要設定才能讓 radio 裡的項目綁定為一組)
- radioModel: 元件被選取後要綁定的 scope 變數
- radioChange: 元件變更選取項目時要觸發的 function
   
#### - radioData 物件格式
- text: [string] 要顯示的文字
- value: [*] 點選後的值 (radio 的 value)
- checked: [boolean] 是否選取
- disabled: [boolean] 是否無法點選
   
#### 使用範例
```
$scope.changeRadio = (data, event) ->
  console.log "selected data=", data
  console.log "selected event=", event
  # 測試 radio-data 的雙向綁定
  $scope.petRadioDataList[0].disabled = true
  $scope.petRadioDataList[1].disabled = false
  $scope.petRadioDataList[1].text = "Pika"
  $scope.petRadioDataList[1].value = "pika"
  # 測試 radio-model 的雙向綁定
  $scope.target.age = ">=20"
  return

$scope.sexRadioDataList = [
  {text: "Man", value: "man"},
  # 測試兩個 item 裡面都有 checked= true
  {text: "Woman", value: "woman", checked: true}
  {text: "Other", value: "", checked: true}
]

$scope.ageRadioDataList = [
  {text: "<12", value: "<12"}
  {text: "<20", value: "<20", checked: true}
  {text: ">=20", value: ">=20"}
]

$scope.petRadioDataList = [
  {text: "Dog", value: "dog", disabled: true}
  {text: "Cat", value: "cat", disabled: true}
]

$scope.target = {
  # 值故意和 $scope.ageRadioDataList 裡 checked 的 value 不一樣
  age: "12"
  pet: ""
}
```
```
div
  | Sex(不綁 radio-model):
  spane(ng-repeat="sexRadioData in sexRadioDataList")
    basic-radio(radio-name="sex", radio-data="sexRadioData", radio-change="changeRadio")
div
  | Age:
  div(ng-repeat="ageRadioData in ageRadioDataList")
    basic-radio(radio-name="age", radio-data="ageRadioData", radio-model="target.age")
div
  | Pet:
  div(ng-repeat="petRadioData in petRadioDataList")
    basic-radio(radio-name="pet", radio-data="petRadioData", radio-model="target.pet")
div
  | {{target}}
```
