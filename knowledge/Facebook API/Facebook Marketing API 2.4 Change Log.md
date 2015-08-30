# Facebook Marketing API 2.4 Change Log

## 最後通牒
請在 2015/10/07 前更新，不然就哭哭了。

## 新功能
1. Labels API
2. 新的 `app_install_state` 欄位

## 改動
1. 出價方式簡化，請參考 [Facebook Marketing API 2.4 Bid Simplification](https://github.com/TMDer/warehouse/blob/master/knowledge/Facebook%20API/Facebook%20Marketing%20API%202.4%20Bid%20Simplification.md)
2. 改動 `CPC Click` 的計算方式：  
以前不小心點到廣告都算 Click，未來只有點到 Link Click 才 +1，廣告主笑了，代操的人哭了。
3. 舊版 `Statistics` 相關的 API 退場：  
未來改用新的 Insights 單一入口樓。
4. Ta 選項優化：  
主要從 ENUM 的方式改爲陣列，想要哪個版位就放進去陣列裏。
5. 舊版 `Ad Tags` API 退場：  
未來就改用 Labels API。
6. 增加`出價最低`限制：  
臺灣地區有幸被列爲兩倍地區，通貨膨脹的力量不可小覷。
7. 移除使用 Advertiser Email 的 `connectionobjects` Edge
8. 移除 Conversion Pixel 的 Status 狀態
9. sub_type 現在是 `custom audience` 與 lookalike creation 的必要參數
10. Ad account TOS 回傳格式更新
11. 移除 AdAccount 內的 `daily_spend_limit`
12. Campaign 內的 spend_cap 從 uint32 改爲數字型的字串
13. Set 內的 `DAILY_BUDGET` `BUDGET_REMAINING` `LIFETIME_BUDGET` 從 uint32 改爲數字型的字串

## 結論
主要就是改動 Click 的計算規則，與出價方式。從花錢林貝是大爺的力場來說，就是漲價了嘛。