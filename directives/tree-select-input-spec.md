# Tree select input
### Dependency Packages
* angular-tree-control
* basicInput

## Usage
**In Angular Controller**

	$scope.inputParam =
		placeHolder: "i am placeholder"
      	notice: "Enter your page, app, or event names"
		filterComparator: false
		dataKey: "name"
		notice: "kk"
		pattern: /[0-9]/
		noticeColor: "red"

	$scope.treeOptions =
		dirSelectable: false
		...

	$scope.treeobject = {}

	$scope.treeSelectData = []

	$scope.treeSelect = (node, selected) ->
		console.log "node = ", node, selected
		return

	$scope.treeInputChange = (inputValue, error) ->
		console.log "input value = ", inputValue, error
		return

	$scope.changeTree =  ->
		$scope.dataForTheTree = [
          {
            "name": "New Tree1"
            "id": "005"
            "age": "21"
            "tooltip": "333"
            "children": []
          }
          {
            "name": "New Tree1"
            "id": "0013"
            "age": "29"
            "tooltip": "gg"
            "children": []
          }
		]

	$scope.dataForTheTree = [
	    { "name" : "Joe", "id": 001, "tooltip": "333", "age" : "21", "children" : [
	        { "name" : "Smith", "id": 011, "tooltip": "333", "age" : "42", "children" : [] },
	        { "name" : "Gary", "id": 012, "tooltip": "333", "age" : "21", "children" : [
	            { "name" : "Jenifer", "id": 121, "tooltip": "333", "age" : "23", "children" : [
	                { "name" : "Dani", "id": 1211, "tooltip": "333", "age" : "32", "children" : [] },
	                { "name" : "Max", "id": 1212, "tooltip": "333", "age" : "34", "children" : [] }
	            ]}
	        ]}
	    ]},
	    { "name" : "Albert", "id": 002, "tooltip": "333", "age" : "33", "children" : [] },
	    { "name" : "Ron", "id": 003, "tooltip": "333", "age" : "29", "children" : [] }
	];
	
	$scope.initTreeSelectedData = [{id: "005"}, {id: "003"}]
	
	$scope.treeSelect = (node, selected) ->
	    console.log "node = ", node, selected
	    return

**In jade Template**

	tree-select-input(input-param="inputParam", tree-options="treeOptions", tree-data="dataForTheTree", no-button="false", on-select="treeSelect", selected-data="treeSelectedData",
	 init-selected-data="initTreeSelectedData", filter-comparator="inputParam.filterComparator", tree-object="treeobject", on-input-change="treeInputChange")

## Tree data syntax
欄位可以自由設定，但是一定要配合使用 input-param 中的 dateKey 參數。其中子項目的資料，一定要用`children`欄位來包裝(array)。而且每筆資料都必須要有`id`欄位，其值不能相同。其中可以對每筆資料設定`tooltip`，其欄位就是`tooltip`。


## Attributes
* `input-param`：  
	*optional*，parameter about input，it can set `placeholder`  
	`notice`：設定 notice 所顯示的資訊  
	`dataKey`：設定 treedata 要顯示出哪個欄位的資料  
	`pattern`：設定 input 欄位的正則表達式  
	`noticeColor`：設定 notice 訊息的顏色，支援`red`和`green`，當沒有設定時，會預設黑色  
	
* `tree-options`：  
	*optional*，this parameter is as same as options parameter at [angular-tree-contorl](https://github.com/wix/angular-tree-control#usage)。

* `tree-data`：  
	**required**，用來設定 tree 的資料。跟 input-param 中的 dateKey 必須配合使用，缺一不可。
	*optional* 給 disabled: true 的屬性， tag 就會有 disabled 的效果（範例如下）
	```
	example : [
	   {id: 1111, name: "沒有 disabeld 效果的藍色 tag"},
	   {id: 1111, name: "有 disabeld 效果的深灰色tag", disabled: true}
	]
	```
	
* `filter-comparator`：  
 default is `false`. The filter comparator is used in determining if the expected value (from the filter expression) and actual value (from the object in the array) should be considered a match.  
	`false`：it looks for substring match in a case insensitive way (the default).  
	`true`：it looks for exact match. 

* `no-button`：  
	*optional*。(Boolean)，預設為`false`。值為`true`的話，會隱藏 toggle tree 的按鈕。

* `selected-data`：  
	**required**，用於綁定被選取項目的資料，格式為 array

* `init-selected-data`：  
	*optional*。可以設定預設備綁定的資料，其資料格式帶入已選項目的`id`即可。

* `tree-disable`：  
	*optional*，會設定 tree 是否可用 enable 或 disable(Boolean)。

* `on-select`：  
	*optional*，當選取項目時會執行的 function，回傳的參數會有項目的資料和是否被選取的 boolean 值。
	`true` 是被選取，`false`反之

* `tree-width`：  
	*optional*，設定套件的寬度。
	
* `tree-object`：  
	*optional*，可以讓 directive 綁定的 object，會提供`selectedNode(node, selected)`的 function  
	`selectedNode`：`node`的格式跟`init-selected-data`要帶入`id`欄位，`selected`為 boolean，設定是否被選曲
	`mappingSelectedDataToDisabled`：第一個參數傳入要找尋的 tree data，第二個參數傳入要被選取的 data。

* `on-input-change`：  
	*optinoal*，當 input 有輸入資料的時候會執行的 function，會回傳 input 正在輸入的值和 pattern 的測試結果。

* `open-insert`：  
	*optional*，支援可以透過 enter 就增加到 tag 







