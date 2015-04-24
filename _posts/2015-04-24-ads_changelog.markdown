---
layout: post
title:  "Facebook Ads API 2.3 重要變更"
date:   2015-04-24 12:36:07
categories: warehouse work flow
tags: work flow
image: https://contentequalsmoney.com/wp-content/uploads/media/2013/10/facebook-api-.jpg
---

## Facebook Ads API 2.3 重要變更

目前 2.2 API 版本可以使用至 `2015/07/08` ，之後將正式啟用 API 2.3 ，總項目修改細節歸納如下，


### objective 變革

`objective` 現在只存在 Ad Campaign 內，以往是可以再透過 Ad Group 設定，接下來 2.3 改版之後將無法使用。

2.3 版本後，如果 Ad Campaign 底下 的 objective 是 `NONE` 的 ，然後在 Ad Group 設定 objective，廣告雖然會繼續投遞，但是就不能再加任何廣告進這個 Ad Campaign 了。


### 時區變革

時間格式現在帶有`時區`了，以前時間如果沒有設定參數， Facebook Ads 會根據使用者時區補上資料，改版之後都要傳入帶有時區的參數，不然就用 Unix Timestamp，否則會判斷為傳入參數錯誤。

### 影片上傳方式改善

新的影片上傳方式：不用再把整個影片上傳，可以分段。

### 規格更新

`OFFER_CLAIM` 的 `promoted_object` 規格變了：以前要放入 offer_id ，但是現在請放 `page_id`，不過已經上傳的 Ad Set 不需要手動更新。
 
### 原始參考資料,

 * [Facebook API Changelog](https://developers.facebook.com/docs/marketing-api/changelog)