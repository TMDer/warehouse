# Tag Directive Usage

## UI
* Tag enable 狀態  
![Tag enable](./directive-images/tag-enable.png)

* Tag disabled 狀態  
![Tag disabled](./directive-images/tag-disabled.png)

## Syntax
	tag(tag-text="tag 的 message" tick-up="點擊後執行的程式" tag-status="tag 狀態")

### tag-text：
tag 上所顯示的 message

### tick-up：
點擊 tag 後面 X 按鈕後會執行的 function

### tag-status：
　如果是 true  則會是 enable 狀態  
　如果是 false 則會是 disabled 狀態  
