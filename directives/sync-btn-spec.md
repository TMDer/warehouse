# Sync Btn

#### Module Name
common.syncBtn

#### 參數說明
* on-click(required): 按鈕觸發函式
* is-async(required): 是否同步中 true /false
* type: 按鈕顏色 success， default is empty
* tip: tooltip 的文字
* tip-placement: tooltip 顯示位置 left / right / top / bottom

#### 使用方式
```
    sync-btn(on-click="syncClick()" is-async="syncBtn")\
    sync-btn(on-click="getUserAdAccount()" is-async="syncBtn" type="success" tip="{{'global-profile-sync' | translate}}" tip-placement="left")
```
