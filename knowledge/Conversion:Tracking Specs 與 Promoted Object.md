# Conversion/Tracking Specs 與 Promoted Object

## 一切都與錢有關

Conversion Specs 跟錢很有關，以下兩個狀況會使用到 Conversion Specs，一是使用 CPA ，二是使用 oCpm 且設定了 Action 價格，其中兩種適用條件的共同點就是 `Action`，如果花錢如流水的基礎，是根據每個 Action 去計價，那勢必要先清楚知道 Action 的定義，到底是按了粉絲專頁(Page)上的讚？還是安裝一個小豬鋪滿的 App 叫 Action？若不先定義清楚什麼是 Action ，就無法正確出價。

所以建立廣告時，應該要有對應的 Conversion Specs，確保對於 Action 的定義是正確的，但目前 Facebook 的設計，其實並不需要傳 Conversion Specs，Facebook 有自己預設的 Conversion Specs，除非有特殊的應用需求需要自定，才會複寫預設的 Conversion Specs。

舉個例子，我們想要主打某個貼文(Post)，希望大家都能感應到這篇貼文(Post)。不論是點一下讚，還是到處分享騷擾朋友，甚至只是想看看上面的美女圖，這些動作都是我們花錢如流水的目標。所以 Facebook 會幫我們自動產生一組 Conversion Specs: 

```
{'action.type':
'post_engagement', 
'post':'POST_ID', 'page':'PAGE_ID'}
```
透過這樣告訴 Facebook ：「這個廣告競價的 Action 就是 post_engagement ，而且我說的就是星期天購物裏面要賣阿帕契直升機模型的那篇貼文(Post)。」

## 可能跟錢比較沒有關
Tracking Specs 跟錢比較沒有關，與 Conversion Specs 比起來，只是純計算，記錄廣告的 Action 有多少，但遇到一樣的問題，什麼是 Action ？Tracking Specs 定義的是你想追蹤的 Action ，也因爲跟出價無關，所以就不限制使用什麼出價方式。

## 一些小祕密
Conversion Specs 與 Tracking Specs 兩位好兄弟的關係不太好，同樣的 Specs 只能給某一個人，如果兩邊都放了，只有 Conversion Specs 會有。
如果想傳入 Conversion Specs 代替預設值，原先 Facebook 產生的 Conversion Specs 會消失，以你傳入的爲主。
如果是想傳入 Tracking Specs ，則會變成是以附加的方式黏到後面，但對於 NONE 或者是 App Install/Engagement Object 類型又例外。

## 改版後的新 Boss
Facebook 在更新了三層架構後，在 Ad Set 層級加了一個項目叫 Promoted Object ，而且在某些 Objective 還是必填，以下是必填的 Objective 類型：

* WEBSITE_CONVERSIONS
* PAGE_LIKES
* OFFER_CLAIMS
* MOBILE_APP_INSTALLS
* CANVAS_APP_INSTALLS
* MOBILE_APP_ENGAGEMENT
* CANVAS_APP_ENGAGEMENT

其實以上項目原先都在 Conversion Specs 會做設定，一旦在 Promoted Object 設定過後， Conversion Specs 的設定參數都會由 Promoted Object 的設定去產生，但 Promoted Object 在以上 Objective 又是必填，他的意思是新改版的 Boss 等級比較高，所以遇到以上 Object 請愛用 Promoted Object 。

## 你認真的？
當然不是， Promoted Object 是驗證機制，在古代，地球人會在投遞完某隻廣告後，把從原本推廣安裝星期天購物APP，改成推廣女性經期記錄APP，但又沒有建立一個新的 Ad Set，進而導致了恐龍滅絕，由於 Facebook 廣告系統的設計，Ad Set 下面的 Ad Group 是可以替換掉，雖然一直宣傳替換的時候，不要這樣做，但許久不見成效，爲了避免這個問題，現在有了 Promoted Object ，如果你再嘗試着把完全不一樣的 Ad Group 做替換...總之你不該這麼做。

## 新 Boss 的技能？
1. 如果是 App 相關 Object，需要先在 Application Settings 內設定相關資料。其中的 object_store_url 必須與你想 Promote 的 App 是同一個，而且素材(Creative)內設定的網址也要一樣。
2. 如果是跟粉絲專頁(Page) 有關，素材(Creative)內的設定也要一致。
3. 以上提到的所有東西，包還一個沒提到的 pixel_id ，一定要跟你的帳號有關聯，且你的帳號有足夠的權限，不然就會 GG 。
4. 這是一個永久性的設定，一旦建立完就不能在更改，但有規則就有例外，pixel_id 沒有這個限制。其餘若真的需要變更。請建立一個新的 Ad Set。
5. 建立好的 Ad Set 不能加入 Promoted Object ，只能建立一個新的。
6. 有 Promoted Object ，就沒有 Conversion Specs 。





無關的補充(還沒找到地方放)：10%限制：調整budget不得低於已經花費的 110%