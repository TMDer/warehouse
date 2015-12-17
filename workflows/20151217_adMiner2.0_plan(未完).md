
## AdMiner 調整計畫


### ===可獨立調整的部分===

#### NodeModule 整理
清除合併無用的 module, 建立 module使用機制

#### Bootstrap
整理, 確認是否能從 config 獨立

#### initDevelopData
整理, 補充 init 樣本, 確認是否能從 config 獨立

#### Policies / Responses
整理, 調整及確認

#### SpecService
- 建立 Spec 架構及初步分類   
- 重新確認 Spec 規格   
- 將規格 (hardcode)單一化

#### Unit
- 建立架構及初步分類
- 整理合併 TaskQueueService / SocketService / ParseService....到 Unit
- 補充系統功能, 如 Session / SystemMsg...等等

### Spec 優化
- 訂立方便建立 spec 及 trace 的架構及流程   
   
### ===會影響目前功能的部分===

#### Controllers
- 移除無用的 api
- 將邏輯處理的部分移到 service
- 套用新的 responses / Unit

#### FbService
- 整理
- 套用 Unit

#### Service
- 階段性將 一般 Service 做重構(rebuild), 並以需要的 DbService
