# 問題思考 - Better way

##問題

```coffee
if adgroup_status is "PAUSED" or adgroup_status is "ACTIVE" or adgroup_status is "NOT_DELIVERING" or adgroup_status is "CAMPAIGN_PAUSED"
  # do something
```

有沒有更好的解法！？

## Try

```
canUpdateStatus = ["PAUSED", "ACTIVE", "NOT_DELIVERING", "CAMPAIGN_PAUSED"]
changeStatusIsAllow = fbAdgroupStatus in canUpdateStatus
if changeStatusIsAllow
```

## 更有效率的解法

 * [http://jsperf.com/js-lodash-indexof](http://jsperf.com/js-lodash-indexof)

## 有沒有更好的方法！？

