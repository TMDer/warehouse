## migrate DB with Sails.js
1. Npm Packages  
```
npm uninstall sails-migrations --save  
npm install sails-db-migrate --save  
```
3. Import Database
4. Terminal Command  
```
grunt db:migrate:up
```
5. Rollback Command  
```
grunt db:migrate:down
```

## 碰到的問題和解決方式

1. Migration Packages Testing & Troubleshooting  
  原有的 `sails-migrations` 試圖排除錯誤、設定，還是無法正常運行，  
  **解決方式：** 找尋替代方案，目前選擇：`sails-db-migrate`。  
2. Invalid Database Table Columns Comparison  
  Error message like: `Data truncation: Truncated incorrect XXXXX value: 'xxxxxxxxxxx'`  
  **原因：** Columns types after WHERE clause have to be the same.  
  **解決方式：** 先比較，才變更型態。  
3. Value Swap Between Columns  

  網路上流傳著幾種方式：  
```
  UPDATE table SET table.column1 = table.column2, table.column2 = table.column1;
  UPDATE table SET table.column1 = table.column2, table.column2 = @originColumn1 WHERE @originColumn1 := table.column1;
  UPDATE table SET table.column1 = (@originColumn1 := table.column1), table.column1 = table.column2, table.column2 = @originColumn1"
```

### 參考
- hat  
  https://www.npmjs.com/package/hat
- sails-db-migrate  
  https://github.com/building5/sails-db-migrate
- node-db-migrate  
  https://github.com/kunklejr/node-db-migrate
- db-migrate  
  https://www.npmjs.com/package/db-migrate
- `utf8_unicode_ci` v.s. `utf8_general_ci`  
  http://stackoverflow.com/questions/341273/what-does-character-set-and-collation-mean-exactly
  http://stackoverflow.com/questions/766809/whats-the-difference-between-utf8-general-ci-and-utf8-unicode-ci
