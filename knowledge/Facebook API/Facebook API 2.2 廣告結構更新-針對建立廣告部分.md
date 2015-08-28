
# Facebook API 2.2 廣告結構更新-針對建立廣告部分

--------
# 舊有結構

依序由上往下的包覆結構有三層，分別是：

* Ad Campaign
* AD Set
* Ad Group

這三個類型的物件。

--------

其中每一個每個類型物件，在建立時 API 可接受的參數如下：

### Ad Campaign:

- name
- objective
- campaign_group_status
- execution_options
- buying_type
		
### Ad Set:

- name
- campaign_group_id
- campaign_status
- execution_options
- daily_budget
- lifetime_budget
- start_time
- end_time
- redownload
		
### Ad Group:

- name
- campaign_id
- objective
- adgroup_status
- bid_type
- bid_info
- conversion_specs
- creative
- targeting
- tracking_specs
- view_tags
- social_prefs
- redownload

### Targeting - Location

- countries
- regions
- cities
- zips

--------
# 更新結構

依序由上往下的包覆結構依然有三層，分別是：

* Ad Campaign
* AD Set
* Ad

新的改動如下所列：

--------

### Ad Campaign:

- name
- objective
- campaign_group_status
- execution_options
- buying_type
		
### Ad Set:

- name
- `targeting`
- `promoted_object` 
- `is_autobid`
- `bid_info`
- `bid_type`
- campaign_group_id
- campaign_status
- execution_options
- daily_budget
- lifetime_budget
- start_time
- end_time
- pacing_type
- campaign_schedule
- redownload
		
### Ad: (原名稱爲 Ad Group)

- name
- campaign_id
- objective
- adgroup_status
- <font color="red">*bid_type X (已經移除)*</font>
- <font color="red">*bid_info X (未移除，稍晚失效)*</font>
- conversion_specs
- creative
- <font color="red">*targeting X (已經移除)*</font>
- tracking_specs
- view_tags
- social_prefs
- redownload

### Targeting - Location

- countries
- regions
- cities
- zips
- `custom_locations`
- `geo_markets`
- `location_types`

### Targeting
- `CBT (Broad Category Targeting)`
- `friends_of_connections`
- `promoted_object`

--------

# 整理

主要的大變動有幾項：

1. 把 Ad Group 更名爲 `Ad`。
2. 將原先在 Ad Group 內的 `Bid` (bid_type 與 bid_info) 的設定移動到 Ad Set 內。
3. 增加 `is_autobid` (讓 Facebook 爽爽花你的錢？) 設定，另外想開啓這個欄位， Ad Campaign 的 Objective 不得設爲 NONE。
4. 將原先在 Ad Group 內的 `Targeting` 的設定移動到 Ad Set 內。
5. `Targeting` 的 user_os 可以詳細到系統版本。
6. 在 Targeting 內的 `Location` ，新增更多參數。
7. `Targeting` 增加 `friends_of_connections` 對朋友的連結
8. `Targeting` 增加 `CBT (Broad Category Targeting) ` 自訂叢集建立、管理帳號
9. `Targeting` 新增 `Flexible targeting` ，為彈性的 `Targeing` 利用 and, or 的概念傳輸受眾資料
10. 在 Ad Set 內新增 `promoted_object` ，在特定的 Objective 這個欄位是必須的。


# Promoted_Object

當你的 Campaign 是是以下 Objective 需要帶有 Promoted_Object 屬性

- WEBSITE_CONVERSIONS
- PAGE_LIKES
- OFFER_CLAIMS
- MOBILE_APP_INSTALLS
- CANVAS_APP_INSTALLS
- MOBILE_APP_ENGAGEMENT
- CANVAS_APP_ENGAGEMENT

