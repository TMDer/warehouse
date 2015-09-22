## scss 結構調整

* home.scss
* _variables.scss
* _basic.scss
* _layout.scss
* adminer
  * _index.scss 
  * adMgmt
    * _admgmt.scss
  * trackMgmt
    * _trackMgmt.scss
  * audience
    * _audience.scss
  * report
    * _report.scss
  * dashboard
    * _dashboard.scss
  * editUserProfile
    * _editUseProfile.scss
  * eventLog
    * _eventLog.scss
  * adCreateAndEdit (adCampaign, adCreative, adGroup, adSet)
    * _adCampaign.scss
    * _adCreative.scss
    * _adGroup.scss
    * _adSet.scss
  * user
    * _user.scss
  * common
    * _*.scss


### home.scss

負責 import 所有檔案

### variables.scss

只存放共用變數 (ex. $brand-success: #93be36;)

### basic.scss

我們系統的基本樣式, 以及可以使用的 @mixin, @extend 等等

ex. 

```
// class
.btn {
  outline: none;
}

// extend
%btn{
  outline: none;
}

// mixin
@mixin center-block {
  outline: none;
}

```

### layout.scss

放置 hearder.scss 以及 footer.scss

### adminer資料夾

   style/adminer 資料夾結構如同 template

:: common

共用的 lib 或 directive 的 scss

:: adCreateAndEdit

每個階段的 scss ( adCampaign, adSet, adCreative, adGroup )

:: adminer內的其他的資料夾

目前規劃只會有一個 scss， 並以一個 id 劃分區塊

ex.

```
#audience {

}
#audience-create{

}
#audience-edit{

}
```



