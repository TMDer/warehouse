### Sails Version 0.10.3 Upgrade 0.11.0 and Hot Reload

#### 安裝
安裝好 Sails 0.11.0 版本後，下二個指令 
npm install socket.io-redis@0.1.4 --save 
npm install sails-hook-autoreload

#### 修正「Sails」載入參數
在載入Sails的位置寫入
dontFlattenConfig: true

#### 設定「config/sockets」參數  
棄用「onDisconnect」改以下內容取代  
  
``` node
afterDisconnect: function (session, socket, cb) 
  return cb()
```
adapter: 'redis' 
改為 
adapter: 'socket.io-redis'

authorization: true
改為
beforeConnect: undefined

參考 :: 
http://sailsjs.org/version-notes/0point10-to-0point11-migration-guide
