

# Basic Component

## ::basicButton  
#### Module Name
commonApp.basicBtn


#### 參數說明
* draft: 指定常用的按鈕樣式，會自動套入預設的 color 和 text
* color: 按鈕顏色
* text: 顯示文字
* fa: 按鈕圖示的 class
* disabled: 是否禁止點下按鈕
 
#### draft 項目
pewv / next / cancel / submit / icon-create / icon-delete / icon-copy / icon-edit / icon-sync

#### color 項目
gray(default) / green / purple

#### fa class 參考
https://fortawesome.github.io/Font-Awesome/icons/

#### color 項目
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
basic-btn(color="purple", text="Home", fa="fa-home fa-fw", disabled="true")
basic-btn(color="green", fa="fa-refresh")
basic-btn(color="green", fa="fa-refresh", disabled="true")
```

## ::pmdDropdown  
#### Module Name
common.pmdDropdown


#### 參數說明
* items(required): Dropdown Items ，項目不可重複 (Array)
* selected-osition(required): 目前選擇項目的位置 (String)
* pmd-change: 使用者點選後觸發的動作 (Function)
* defalut-position: 預設顯示的項目 (Int)， default is 0
* disabled: 是否要停用這個物件， default is false
   
#### 使用方式
    
```
    pmd-dropdown(items="trafficValueArgs", defalut-position="0", selected-position="trafficTypePosition" pmd-change="selectedWebsiteTraffic(trafficArgs[trafficTypePosition], trafficTypePosition)")
```

## ::pmdInput
http://stackoverflow.com/questions/14378401/dynamic-validation-and-name-in-a-form-with-angularjs
#### Module Name
common.pmdInput


#### 參數說明
* form(required): 這個 input 的 form 物件
* ngModel(required): 這個 input 對應到的 model
* type(required): 輸入類型 text(文字) / url(網址)
* name(required): 這個 input 在 form 裏面的名稱
* placeholder: 提示輸入訊息
* maxlengthMessage: 超過長度警告訊息
* requiredMessage: 未填入文字警告訊息
* minlength: 最短字數限制
* maxlength: 最長字數限制
* required: 是否爲必填， default is false
* disabled: 是否要停用這個 input， default is false
   
#### 使用方式

```
form.form-horizontal(role='form', name="adCampaignForm")
      pmd-input(type="text", form="adCampaignForm", name="adName", placeholder="Please Input Name", ng-model="adCampaign.name", minlength="1", maxlength="50", required="true", maxlength-message="最長五0個字", required-message="此欄位必填")
      pmd-input(type="'text'", form="adCampaignForm", name="editName", placeholder="Please Input Name", ng-model="adCampaign.title", minlength="1", maxlength="50", required="true", maxlength-message="最長五0個字", required-message="此欄位必填")
      pmd-input(type="'url'", form="adCampaignForm", name="url", placeholder="Please Input URL", ng-model="adCampaign.url", required="true", required-message="此欄位必填")
      pmd-input(type="'url'", form="adCampaignForm", name="url2", placeholder="Please Input URL", ng-model="adCampaign.mpa.url", required="true", required-message="此欄位必填")
      pmd-input(type="'text'", form="adCampaignForm", name="text2", placeholder="Readonly", ng-model="adCampaign.text", disabled="true", required-message="此欄位必填")
```

## ::pmdRadio
#### Module Name
common.pmdRadio


#### 參數說明
* radioData(required): 元件要顯示的物件
* ngModel(required): 元件被選取後要綁定的變數
* name(required): 元件名稱
* pmdChange: 元件變更選取項目時要觸發的方法
* disableAll: 將此元件變更爲不可選取狀態
* defalutPosition: 元件預設選取的項目， default is null

#### 使用方式

```
$scope.radioData = [
      {text: "Daily", value: "daily"},
      {text: "Forever", value: "forever"},
      {text: "One Week", value: "week", disabled:"true"}
    ]
    
pmd-radio(radio-data="radioData", name="dailySetRadio", ng-model="seletecRadio", pmd-change="changRadio()", defalut-position="0")
      
pmd-radio(radio-data="radioData", name="dateRangeSettings", ng-model="seletecRadio", pmd-change="changRadio()", defalut-position="0", disable-all="true")
```

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
