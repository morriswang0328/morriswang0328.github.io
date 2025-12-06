## CANedge 速覽
CANedge 是支援 CAN/CAN FD 的資料記錄器，可將原始總線訊息保存為 MDF/ASC 檔案。

### 常見應用
- 車輛診斷與耐久測試
- 工業設備 CAN 狀態監控
- 航太或機電系統的故障追蹤

## 基本設定
1. 以 Config Tool 建立設定檔並存入記憶卡根目錄
2. 設定 CAN 位元率，必要時啟用 CAN FD 資料階段速率
3. 啟用訊框過濾以降低記錄檔大小
4. 設定檔案輪替大小與 RTC 時區，方便後處理

## 資料存取與轉換
- 取回記憶卡後，優先備份原始 MDF 檔
- 使用 asammdf 或 MATLAB `mdf` 模組將 MDF 轉為 CSV/Parquet
- 若需要 DBC 解析，可在 asammdf 內匯入 DBC 並導出解析後訊號
- 日誌可搭配 `canedge_browser` 或 Grafana 進行可視化

## 最佳實務
- 佈線時確保 120 Ω 終端，並檢查 bus 電壓落差
- 量測同步：在多台 CANedge 上使用 GPS 時戳或 NTP 做時間對齊
- 定期檢查 SD 卡健康度並保留至少 10% 空間，避免寫入延遲
