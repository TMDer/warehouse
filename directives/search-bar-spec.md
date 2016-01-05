# search-bar

#### 參數說明
* queryPlaceholder(required): `String`, search-bar中placeholder的文字
* queryChange(required): `Function(query)`, onChange時會觸發的函式
* query(required): `String`, binding search-bar input內容的變數
* collapsible: `Boolean`, input是否可以開闔
* showInput: `Boolean`, input的初始打開與否

#### 使用方式
```
  search-bar(query-placeholder="{{ 'audience-header-search-place-holder' | translate }}", query="basicSearch"
  , query-change="searchAudienceTableData()")
```
