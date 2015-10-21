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
	    { "name" : "Joe", "age" : "21", "children" : [
	        { "name" : "Smith", "age" : "42", "children" : [] },
	        { "name" : "Gary", "age" : "21", "children" : [
	            { "name" : "Jenifer", "age" : "23", "children" : [
	                { "name" : "Dani", "age" : "32", "children" : [] },
	                { "name" : "Max", "age" : "34", "children" : [] }
	            ]}
	        ]}
	    ]},
	    { "name" : "Albert", "age" : "33", "children" : [] },
	    { "name" : "Ron", "age" : "29", "children" : [] }
	];

**In jade Template**

`tree-select-input(input-param="inputParam" tree-options="treeOptions" tree-data="dataForTheTree")`

### Attributes
* input-param：  
	*optional*，parameter about input，it can set `placeholder`, `notice`, `filter comparator`, `dataKey`  

	`filterComparator` default is `false`. The filter comparator is used in determining if the expected value (from the filter expression) and actual value (from the object in the array) should be considered a match.  
	If `false`, it looks for substring match in a case insensitive way (the default).  
	If `true`, it looks for exact match.  
	
	`dataKey`用來設定 treedata 要顯示出哪個欄位的資料

* tree-options：  
	*optional*，this parameter is as same as options parameter at [angular-tree-contorl](https://github.com/wix/angular-tree-control#usage)。

* tree-data：  
	*required*，用來設定 tree 的資料。其欄位可以自由設定。但是子資料的話，必定要用`children`欄位來包裝。