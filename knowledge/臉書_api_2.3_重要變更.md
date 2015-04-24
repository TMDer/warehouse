## Facebook Ads API 2.3 重要變更

 1. `objective` 現在只存在 Ad Campaign 內：以前可以在 Ad Group 設定，現在不行了，而且，萬一你把一個廣告放在 objective 是 NONE 的 Ad Campaign 底下，然後在 Ad Group 設定 objective，一旦改版，廣告雖然會繼續投遞，但是就不能在加廣告進這個 Ad Campaign 了。
 2. 時間格式現在帶有`時區`了：以前時間如果沒有參數， Facebook 會偷看你的個人資料幫你把時區補上去，現在他們覺得每次都偷看你個人資訊裏的資訊太累了，以後都要傳入帶有時區的參數，不然就用 Unix Timestamp。 
 3. 新的影片上傳方式：不用再把整個影片上傳，可以分段。
 4. `OFFER_CLAIM` 的 `promoted_object` 規格變了：以前要放入 offer_id ，但是現在請放 `page_id`，不過已經上傳的 Ad Set 不需要手動更新。
