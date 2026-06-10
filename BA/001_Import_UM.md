# 物料報表匯入
本系統封箱與拆箱作業流程所需的索引資料，係依據每日人工產製的到貨清單以及UM系統產出的清單組合而成。本次有五個表需匯入：每日到貨清單、InventoryLinesView (InvLines)、WO Header (WO)、Award Line (Awd)、Repair Order Lines (RO)。

## 匯入流程
依據2026.04.28需求確認會議，統整如下：
 ![image](https://hackmd.io/_uploads/ryPip-S-Mx.png)
 
## 檔案交換方式
檔案放置於sftp空間，基嘉系統以排程方式至約定的sftp空間取得檔案。排程時間暫定為每2小時一次。例如UM系統於上午9點執行資料匯出，則DTMS於9點20分啟動排程，開始從sftp取檔轉檔。上線前可視實際情況調整。
 
## 檔案命名原則
路徑 & 檔案名稱如下，每次產出檔名不同，不會覆蓋。
├── Inbound                                     # 到貨清單
│   └──inboundYYYY_MM_DD_HH_MM_SS.xlsx
├── UM                                          # UM系統產出
│   ├──DTMS AwardLineYYYY_MM_DD_HH_MM_SS.xlsx
│   ├──DTMS InvLinesYYYY_MM_DD_HH_MM_SS.xlsx
│   ├──DTMS RepairOrderLinesYYYY_MM_DD_HH_MM_SS.xlsx
│   └──DTMS WO HeaderYYYY_MM_DD_HH_MM_SS.xlsx


## 資料篩選方式
五個表將保留欄位如下，其餘欄位可以剔除
![image](https://hackmd.io/_uploads/S1LT0ZrWzl.png)

### 轉換條件
UM系統只能以日期區間匯出資料，無法判斷該筆資料是否已匯出，故轉入DTMS系統時，需要先做過濾以及比對。


| 資料表 | 限制條件 | 比對條件，完全符合即為重複 |
| -------- | -------- | -------- |
| inbound    | 無須篩選     | Award NO、Line、Part Number、MAWB、HAWB、實際送達日、報單號碼    |
| AwardLine  | Status=open |Award No、Line、Item、status |
| InvLines    | Commit=true|Trx No、Commit Date、Line、Item、GRN、Serial、Deferral ID、PO、Award Line |
| RepairOrderLines    | Status=open|Trx No、Line、Repair Item、Repair Serial、Qty Received、Fully Rcvd、Status Code、Line Status     |
| WO Header| Main rqmt=CAL |Work Order、serial、part、Maint Rqmt |


