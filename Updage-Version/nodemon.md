### nodemon 安裝說明
安裝  
npm i nodemon -g  
  
在專案根目錄下建立「nodemon.json」，內容如下  
``` json
{
    "watch": [
        "api/"
    ],
    "ext": "js jade coffee"
}
```

專案下執行指令
sudo nodemon app.js

解安裝指令
npm uninstall nodemon -g
