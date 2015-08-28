# Facebook Marketing API 2.4 Bid Simplification

## 說明
以前的出價方式與 API 對應不上容易誤導，所以 Facebook 重新設計 API 的出價設定讓他更直觀與簡單。

## 變更
1. 移除 `bid_info` 與 `bid_type` 兩個欄位寫入方式。
2. 新增 `billing_event` 與 `optimization_goal` 以及 `bid_amount` ，三個欄位。
3. 移除 `mixed bid_info` 出價方式，未來只能針對想優化的項目出價。

## 出價對應表
| v2.3 bid_type | v2.4 billing_event | v2.4 optimization_goal |
|:-------------:|--------------------|------------------------|
| CPC           | CLICKS             | CLICKS                 |
| CPM           | IMPRESSIONS        | IMPRESSIONS            |
| ABSOLUTE_OCPM | IMPRESSIONS        | ANY                    |
| CPA           | APP_INSTALLS       | APP_INSTALLS           |
|               | PAGE_LIKES         | PAGE_LIKES             |
|               | OFFER_CLAIMS       | OFFER_CLAIMS           |
|               | LINK_CLICKS        | LINK_CLICKS            |
|               | POST_ENGAGEMENT    | POST_ENGAGEMENT        |

## 結論
不論怎麼變更，真正的差別是移除 `mixed bid_info` 出價方式。

## 參考資料
[Facebook v2.4 Optimization Simplification](https://developers.facebook.com/docs/marketing-api/optimization_simplification#backwards "Title")