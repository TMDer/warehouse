# Step Widget Spec
### 用法
`step(step-title="titleData" disabled="stepDisabled" edit-click="stepClick()" is-finish="stepStatus" item-list="itemList")`

### 所需參數及格式
* step-title：傳入步驟的順序及標題

		titleData = {
			number: 1
			text: "Choose Campaign Objective"
		}

* edit-click：傳入點擊編輯按鈕後會執行的函式  
	![Step icon](./directive-images/step-edit-icon.png)

* disabled：控制 step 的狀態，值為 Boolean  
	**true**  
	![Step disabled](./directive-images/step-disable.png)  
	**false**  
	![Step enable](./directive-images/step-process.png)

* is-finish：控制 step warn icon 的狀態，值為 Boolean  
	**true**  
	![step finish](./directive-images/step-finish-icon.png)   
	**false**  
	![step warn](./directive-images/step-warn-icon.png)  
	
* status：控制 step 的狀態，值為 default, disable, process
	* default：僅僅觀看此步驟資訊  
		![default](./directive-images/step-default.png)
	* disable：還未進入過此步驟  
		![disable](./directive-images/step-disable.png)
	* process：正在此步驟時  
		![process](./directive-images/step-process.png)