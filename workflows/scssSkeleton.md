## scss 結構調整

* home.scss
* pmd.scss
* variables.scss
* basic.scss
* layout.scss
* adminer
  * adMgmt
    * admgmt.scss
  * trackMgmt
    * trackMgmt.scss
  * audience
    * audience.scss
  * report
    * report.scss
  * dashboard
    * dashboard.scss
  * editUserProfile
    * editUseProfile.scss
  * eventLog
    * eventLog.scss
  * operator
    * operator.scss
  * AdCreateAndEdit (adCampaign, adCreative, adGroup, adSet)
    * adCampaign.scss
    * adCreative.scss
    * adGroup.scss
    * adSet.scss
  * user
    * user.scss
  * common
    * *.scss
 
以一個 id 劃分區塊

ex.

```
#audience {

}
#audience-create{

}
#audience-edit{

}
```

style/adminer 資料夾結構如同 template
