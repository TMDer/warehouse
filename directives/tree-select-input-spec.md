# Tree select input
### Dependency Packages
* angular-tree-control
* basicInput

### Usage
**In Angular Controller**

	$scope.inputParam =
		placeHolder: "i am placeholder"
      	notice: "Enter your page, app, or event names"
		filterComparator: false
		dataKey: "name"

	$scope.treeOptions =
		dirSelectable: false
		...

	$scope.dataForTheTree = [
	    { "name" : "Joe", "id": 001, "age" : "21", "children" : [
	        { "name" : "Smith", "id": 011, "age" : "42", "children" : [] },
	        { "name" : "Gary", "id": 012, "age" : "21", "children" : [
	            { "name" : "Jenifer", "id": 121, "age" : "23", "children" : [
	                { "name" : "Dani", "id": 1211, "age" : "32", "children" : [] },
	                { "name" : "Max", "id": 1212, "age" : "34", "children" : [] }
	            ]}
	        ]}
	    ]},
	    { "name" : "Albert", "id": 002, "age" : "33", "children" : [] },
	    { "name" : "Ron", "id": 003, "age" : "29", "children" : [] }
	];
	
	$scope.initTreeSelectedData = [{id: "005"}, {id: "003"}]

**In jade Template**

    tree-select-input(input-param="inputParam", tree-options="treeOptions", tree-data="dataForTheTree", no-buton="false",
     selected-data="treeSelectedData", init-selected-data="initTreeSelectedData", filter-comparator="inputParam.filterComparator")

### Attributes
* input-param：  
	*optional*，parameter about input，it can set `placeholder`, `notice`, `dataKey`  
 	
	`dataKey`用來設定 treedata 要顯示出哪個欄位的資料
* tree-options：  
	*optional*，this parameter is as same as options parameter at [angular-tree-contorl](https://github.com/wix/angular-tree-control#usage)。

* noButton：  
	*optional*。(Boolean)，預設為`false`。值為`true`的話，會隱藏 toggle tree 的按鈕。

* tree-data：  
	**required**，用來設定 tree 的資料。其欄位可以自由設定。但是子資料的話，一定要用`children`欄位來包裝(array)。而且每筆資料都必須要有`id`欄位，其值不能相同。
* selected-data：  
	**required**，用於綁定被選取項目的資料，格式為 array
* init-selected-data：  
	*optional*。可以設定預設備綁定的資料，其資料格式帶入已選項目的`id`即可。

* filter-comparator：  
 default is `false`. The filter comparator is used in determining if the expected value (from the filter expression) and actual value (from the object in the array) should be considered a match.  
	`false`：it looks for substring match in a case insensitive way (the default).  
	`true`：it looks for exact match. 
