## Angular Performance Boost


### ::簡介

在開發 PMD 的時候，如果是前端頁面，會有 Jade 檔案(View)，以及跟這個 Jade 檔有關的 Coffee 檔案 (Controller)，通常遇到很明確的狀況，例如一個 Input，理應是屬於 View 的範疇，而這個 Input 內容若有變更要進行處裏，則屬於 Controller 的範疇，因此通常會把單純跟顯示在畫面上有關的事物放入 View ，而需要邏輯運算則放入 Controller。前端所有的 DOM 物件操作，成本極高，需要處處計較。總歸一句，把 Controller 與 View 做出正確的切割，以及降低操作 DOM 物件，或是降低操作 DOM 物件帶來的影響，都是在提升順暢度，進而提升使用者體驗非常重要的一環。以上所遇到的問題，主要與切割 View  Controller ，以及降低前端 DOM 物件操作的影響相關聯。

### ::View 與 Controller 劃分

許多有明確範疇的物件並不太會有問題，但些狀態則較不好區別，遇到這類狀況，應盡量把需要運算的邏輯置於 Controller 內，只留下最簡單與必要的邏輯在 View。

1. 範例A：
假設需要把某個廣告的 Status 轉換成比較好看的格式顯示在前端，並且根據這個 Status 決定切換按鈕是否要顯示。

在`範例A`裏面，有兩件事情跟邏輯有關:

1. 根據特定格式轉換 Status 的 Formate
2. 根據 Status 決定是否要顯示切換按鈕

也因爲這兩件事情都有一定成本，在前端都非常的貴，最好的方式就是通通不要在前端處裏，但是(2)提到的根據某個情況決定是否顯示按鈕，則因爲牽涉到前端顯示，顯然有必要在前端進行 ngIf 或 ngShow 的邏輯判斷，換句話說，這是非常難以避免的。但是若是要處裏(1)根據特定格式轉換 Status 的 Formate，可以在取得這筆資料的時候先行轉換，也可在前端要顯示的時候在呼叫特定的轉換函式進行這個功能。對於這類的狀況，可以自由選擇在 Controller 先把資料 Format ，或是在前端要 Render 畫面時，在透過處裏的函式轉換。這類可以在 Controller 處裏完的工作，可以優先以 Controller 爲主。如此一來就可以降低成本，後端的邏輯處裏相對於前端更便宜。

### ::前端邏輯的代價
以下是在 Pmd AdMgmt 畫面上的前端程式碼，在第一次 Loading 畫面，與切換分頁，或是切換 Ad Effect 的時候，都會發生明顯的延遲：

```
.panel.panel-default.base-container.adlist-panel
  table.table.adlist-table(ng-table="adMgmtTableParams" template-pagination="custom/pager")
    thead
      ...
      中間省略
      ...
    tbody
      tr(ng-repeat="adCampaign in $data ", ng-class="{'active': adCampaign.checked}")
        td(data-title="'Type'")
          circle-btn(color="color", target="adCampaign", after-check="checkAd()")
        td(data-title="'Result'" ng-switch="adCampaign['suggestion'].type")
          i(class="fa fa-arrow-up" ng-click="openSuggestionModal(adCampaign)" ng-switch-when="1")
          i(class="fa fa-arrow-down" ng-click="openSuggestionModal(adCampaign)" ng-switch-when="2")
          span(ng-switch-default) --
        td(data-title="'Name'" sortable="'name'")
          span.is-pointer(ng-click="openPreviewModal(adCampaign)") {{adCampaign['name']}}
        td.rowStatus(data-title="'Status'")
          div.toggle-bg(ng-class="adCampaign.toggleAdStatusView", ng-click="toggleAdStatus(adCampaign)")
            input(type='radio', value="on", ng-model="adCampaign.toggleAdStatusView", ng-disabled="isDisabledAdStatus(adCampaign.status)")
            input(type='radio', value="off", ng-model="adCampaign.toggleAdStatusView", ng-disabled="isDisabledAdStatus(adCampaign.status)")
            span.switch(ng-class="adCampaign.toggleAdStatusView")
          div.status-info
            span(ng-bind-html="stringReplace('lineFeed', adCampaign['status'], '_')")
        td.number-field(ng-repeat="tableHead in noFixedTableHeads", ng-switch="tableHead.key")
          .split-column(ng-switch-when="result1")
            div {{adCampaign[tableHead.key].value}}
            div {{adCampaign[tableHead.key].name}}
          .split-column(ng-switch-when="result2")
            div {{adCampaign[tableHead.key].value}}
            div {{adCampaign[tableHead.key].name}}
          .split-column(ng-switch-when="cpa1")
            div {{adCampaign[tableHead.key].value}}
            div {{adCampaign[tableHead.key].name}}
          .split-column(ng-switch-when="cpa2")
            div {{adCampaign[tableHead.key].value}}
            div {{adCampaign[tableHead.key].name}}
          .startDate(ng-switch-when="startDate" ng-bind-html="stringReplace('lineFeed', adCampaign[tableHead.key], '_')")
          .endDate(ng-switch-when="endDate" ng-bind-html="stringReplace('lineFeed', adCampaign[tableHead.key], '_')")
          div(ng-switch-default) {{adCampaign[tableHead.key]}}
```

其中造成延遲的原因有幾項: (依照影響程度排序)

1. ngRepeat + 巢狀 ngRepeat:  
如果說王品牛排很貴，A Cut 還要貴上三倍。而 ngRepeat 比 A Cut 絕對還要貴上五倍 ! 一個巢狀的 ngRepeat ，又比一般的 ngRepeat 貴上兩倍有餘了...


2. 巢狀 ngRepeat + ngSwitch:
如果說請一客王品牛排很貴，請一客王品牛排的同時再請一客 A Cut 的 40oz 的美國頂級BRANDT乾式熟成帶骨肋眼牛排，就是這麼貴阿(尖叫~~~)，由於 ngRepeat 是一個迴圈的邏輯，巢狀的結構會導致執行次數被放大，而裏面搭配的 ngSwitch 則增加了邏輯運算的複雜度。

3. 數量關鍵:  
貴鬆鬆的 A Cut 在貴，還是一份 A Cut ，但如果 50 份 A Cut 加總....就...!目前 Ad Mgmt 在一次顯示五十筆資料的情況下會出現非常明顯的延遲現象。


4. 前端 Binding 資料與函式:  
前端的每個 Angular 變數預設都是 Two-Way Binding，需要被 Watch，顯示這筆資料當下，一同運算邏輯，雖然影響並非甚大，但是省一塊是一塊。

### ::掃雷訣竅

1. [忍住不要買] 別用 ngRepeat:  
買了就是要錢，如果不需要就別用 ! 可以在不用 ngRepeat 而達到一樣的效果，就不應使用 ngRepeat。
2. [殺價] 使用 [track by] *1*:  
該買的都得買，但是如果有幾樣可以打個五折，省下來也不少 ! Angular 1.2 版以來，提供了 track by 功能，在以前只要更新 ngRepeat biding 的資料，ngRepeat 會進行 DOM 的操作。換句話說，即使更新後資料完全一樣，ngRepeat 也會毀滅所有的 DOM 再重做，透過 track by 指定 uid 後，ngRepeat 會在陣列內加入 hash 值，例如本來畫面上有 50 筆依照員工編號排序的員工資料，而使用者點選了只顯示女生，但剛好這間公司全部都是女生，所以剛剛的五十筆跟現在的五十筆完全一樣，有了 track by ，與 hash 值可以比對，且資料剛好一致，什麼都不用做，居然差不多免費誒。就算資料有部分變更，只要針對新物件產生新的 DOM，原本有的需要改變位置而不用重做，效能便可得到提升。
3. [養樂多不要配香腸] 小心特殊的巢狀組合:  
養樂多好喝，香腸好吃，聽說一起吃下去會中毒是真的嗎 !? ngRepeat 與 ngSwitch 未必那麼惡毒，但是一個 ngRepeat 再包裝一個 ngRepeat 搭配 ngSwitch 就會致命，應該要注意是否有因爲組合使用這些邏輯，導致這種出乎意料的狀況。(當然，用越少風險越低)
4. [無息分期] 前端的粗重工作可以少量多餐:  
現金買一臺 Macbook Pro Retina 頂規，接下來就得吃土，但如果刷卡無息分期，至少還可以吃泡麵 ! 每個前端操作都很寶貴，如果免不了得做，分幾次輕一點的工作，總比一次做完的好。
5. [儲蓄] 提前把資料處裏好:  
急用錢在調頭寸，不如先準備好 ! 前端的資料若在收到的當下，進行資料處理，轉換成需要的形式，前端只需要很單純的把資料顯示出來，避免要顯示時在運算，前端畫面的所有操作都很貴。
6. [花在刀口上] 使用 [One-Time Binding] *2* *3*:  
很多東想買，只買必要的就好 ! 每個被 Angular Two-Way Binding 的變數，會一直在整個生命週期內不斷的去 Watch，但是有很多東西只要經過邏輯後顯示到畫面上，就不需要及時性的更新，例如，員工系統內的員工資料總覽，每個員工的資料只要顯示在畫面上就不可能會被更改(就算改動了也沒有及時更新的必要性)，但畫面上這樣的資料或許有一百筆，是從變數拉過來顯示的，只要透過 One-Time Binding ，一旦正確取得員工資料並且被 Binding 到畫面上對應的變數，這個 Binding 關係會立刻消失，畫面也會顯示正確的資料，並且也不再需要持續的去 Watch 這個變數。

### ::藥方 (已經先試喝過)
無息分期的 `limitTo` :
因爲 DOM 物件的操作實在是太貴了，我們也沒辦法送給我們尊貴的客戶一人一臺 Macbook Por 頂規，Angular 更不打算給我們折扣，就只好分期付款了。在使用 ngRepeate 的時候，設定 limitTo 參數，可讓前端顯示的部分有上限，且這個設定可以 binding 到一個變數，動態的更動這個上限，這裏有一個特性，limitTo 只對畫面有影響，對邏輯與資料本身不影響。換句話說， limitTo 多少，畫面在 render 的時候就會顯示多少筆，被 binding 的變數不會被更動。由於第一次載入畫面的筆數比較少，畫面很快就會出來了，使用者體驗就可以提升。待畫面看起來`似乎`已經顯示完成後，再把 limitTo 上限提高，便可以把剩餘的資料顯示出來。

前端範例:

```
tr(ng-repeat="adCampaign in $data | limitTo: generalAdsShowLimit track by adCampaign.campaign_id", ng-class="{'active': adCampaign.checked}")
...
 ```
 
後端範例:

```
$scope.init = ->

	$scope.generalAdsShowLimit = 9
	
	setTimeout () ->
		$scope.generalAdsShowLimit = 50
	, 200

```


### ::註解
1. track by，節錄自官方 Document
>If you are working with objects that have an identifier property, you can track by the identifier instead of the whole object. Should you reload your data later, ngRepeat will not have to rebuild the DOM elements for items it has already rendered, even if the JavaScript objects in the collection have been substituted for new ones:

2. One-Time Binding，節錄自官方 Document
>An expression that starts with :: is considered a one-time expression. One-time expressions will stop recalculating once they are stable, which happens after the first digest if the expression result is a non-undefined value (see value stabilization algorithm below).

3. 需要 Angular 1.3 後的版本才有支援



[track by]: https://docs.angularjs.org/api/ng/directive/ngRepeat
[One-Time Binding]: https://docs.angularjs.org/guide/expression
