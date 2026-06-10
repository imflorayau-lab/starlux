---
title: 002_Device

---

# 接收文件行動端


## 目錄
- [接收文件行動端](#接收文件行動端)
  - [功能架構](#功能架構)
  - [拆箱](#拆箱)
  - [封箱](#封箱)
  - [歸檔標籤製作](#歸檔標籤製作)
    - [轉換條件](#轉換條件)
---

## 功能架構
主要提供封箱、拆箱的影像拍攝以及標籤製作。
1.	使用者登入，搭配雙因子認證。
2.	透過 HTML5 APP 操作拍照、錄影等系統作業。
3.	即時上傳影像檔至「文件及影像掃描系統」。
4.	依所依序選擇欄位資訊產生條碼 (依文件屬性規則)。
5.	將條碼資訊執行列印作業，以供後續透過條碼資訊快速將索引資料與文件影像勾稽結合。
![image](https://hackmd.io/_uploads/r1-GoOLWzl.png)

[⬆ 回目錄](#目錄)

## 拆箱
### 拆箱-影像拍攝作業-進口貨

| 介面 | 說明 |
| -------- | -------- |
| ![image](https://hackmd.io/_uploads/B1cx3_I-zl.png)  | 1.	MSWB主提單、HAWB分提單，報單號碼，三者可擇一查詢，亦可三欄位and查詢。<br>2. 對應欄位：<br>到貨日=inbound.實際送達日<br>報單號碼=inbound.Part Number<br>MSWB=inbound.MAWB<br>HAWB=inbound.HAWB| 
| ![image](https://hackmd.io/_uploads/Hy1CAKIZMl.png) |1.選擇符合報單、主分提單條件下的採購資料。進行影像上傳。<br>2.對應欄位<br>採購單號=inbound.Award NO <br>項次=inbound. RO Line<br>報關/系統件號=inbound.Part Number |

### 拆箱-影像拍攝作業-國內貨
| 介面 | 說明 |
| -------- | -------- |
| ![image](https://hackmd.io/_uploads/ryQjxcIWGe.png)| 1.國內貨無報關資料，故報關/主題/分提均寫入固定值：LOCAL/LOCAL/LOCAL。<br>2.對應欄位<br>採購單=Awd.Award NO or RO.TRx NO<br>項次=Awd.Line or RO.Line<br>系統件號=Awd.Item or RO Repair Item |

### 拆箱-影像拍攝作業-Shop Repair
| 介面 | 說明 |
| -------- | -------- |
| ![image](https://hackmd.io/_uploads/rkRWf9L-Mg.png)| 1.SHOP選擇，讀後台倉別代碼設定檔。<br>2.輸入Package ID/WO，帶出PN、SN。<br>3.若SHOP=PME，則Package ID/WO欄位查詢WO.Work Order，帶出Serial, Part<br>4.若SHOP<>PME，則Package ID/WO欄位查詢InvLines.Deferral ID，帶出Item、Seiral。 |

### 拆箱-影像拍攝作業-移倉調撥
| 介面 | 說明 |
| -------- | -------- |
| ![image](https://hackmd.io/_uploads/By66_cLWGe.png) | 1.	移倉調撥，分進口與國內。預設為進口。<br>2.進口<br>A.到貨日預設為當日。<br>B.	報單號碼、MAWB、HAWB擇一輸入。均由[inbound]提供。<br>C.TQ單號由inbound.Award NO 與InvLines.TrxNO同時提供，帶出TQ項次(inbound.Line or InvLines.Line)。<br>3.報關/系統件號=inbound.Part Num。 |

### 拆箱-文件歸檔標籤印製-SDS
| 介面 | 說明 |
| -------- | -------- |
| ![image](https://hackmd.io/_uploads/ryHt8oLWMg.png)|1.假若GRN編號已知，可直接輸入編號查詢CSS資料，帶出來列印。<br>2.設定SDS的語言別：原文、中文<br>3.選擇SDS的劑別，劑別代碼可由管理後台定義。<br>4.設定SDS出版日期。<br>5. 設定完成寫入CSS的SDS
6.假若GRN未知，就重新從inbound & AWARD 查。|

[⬆ 回目錄](#目錄)
## 封箱
### 封箱-影像拍攝作業-外運
| 介面 | 說明 |
| -------- | -------- |
| ![image](https://hackmd.io/_uploads/HJMaYcUbMl.png) | 1.Invoice NO、Line、PN、SN、Note。全人工輸入，無資料來源。<br>2.	拍攝日預設為當日<br>3.Note欄位最多輸入100個中文字。 |

### 封箱-文件歸檔標籤列印-外運
![image](https://hackmd.io/_uploads/S1XcbjIbfg.png) 

前述影像上傳後，CSS已有案件成立，查詢CSS後列印。

[⬆ 回目錄](#目錄)
## 歸檔標籤製作
### 報單
| 介面 | 說明 |
| -------- | -------- |
| ![image](https://hackmd.io/_uploads/HJYw4sLZMx.png)|查inbound後寫入CSS |





[⬆ 回目錄](#目錄)

