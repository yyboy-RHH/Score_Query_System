# 學生成績管理系統 (Student Grade Management System)

## 📝 專案目標與動機
[cite_start]為了解決教育機構日益龐大的學生數據量，以及傳統手工登錄成績速度慢、錯誤率高、加重教師負擔等痛點 [cite: 6, 7, 9, 14, 15][cite_start]。本專案建立一套完整的學生成績數據管理系統，透過 MySQL 數據庫來效率化管理成績，實現成績登記、查詢、計算和統計等功能 [cite: 2, 4][cite_start]。核心解決方案是以 CSV 整批匯入成績，取代單筆手動登錄 [cite: 16]。

## 🏗️ 系統架構設計
[cite_start]本專案採用 Docker 容器化部署，具備環境簡單（虛擬環境避免版本衝突）與一鍵快速部署的優勢 [cite: 84, 92, 93, 94, 95]。
* [cite_start]**開發語言**: Python [cite: 44]
* [cite_start]**關聯式資料庫**: MySQL (Image 版本 5.7.33) [cite: 45, 47, 57]
* [cite_start]**圖形化資料庫管理工具**: Adminer (網頁版介面，運行於 Localhost:8080) [cite: 80, 97, 98, 99]
* [cite_start]**資料庫驅動程式**: `mysqlclient` 套件 (負責建立 Python 與 MySQL 的連接及 SQL 傳輸) [cite: 49, 105, 106, 107, 108]
* [cite_start]**網路架構**: Docker Network (Default) 橋接容器 [cite: 100]

## ✨ 核心功能模組 (Function Modules)

### 1. 資料表建立 (Table Creation)
* [cite_start]透過 Python 腳本直接操作 MySQL，建立名為 `STUDENTS` 的學生資料表 [cite: 111, 135, 146]。
* [cite_start]支援 UTF-8 編碼，確保多國語言無亂碼 [cite: 139, 155]。
* [cite_start]包含欄位：ID (自動遞增主鍵)、NAME、GENDER、CHINESE、ENGLISH、MATH、SOCIAL_SCIENCE、SCIENCE [cite: 152, 161, 163, 165, 167, 169, 171, 173, 175, 177]。

### 2. CSV 批量匯入 (Batch Import)
* [cite_start]支援讀取 `exam_score.csv` 檔案進行批量匯入，大幅提升處理效率 [cite: 121, 186, 187, 197, 207]。
* [cite_start]具備防呆機制，腳本會自動跳過 CSV 第一行的標題列 [cite: 188, 199, 200]。
* [cite_start]內建錯誤處理機制 (Try-Except)，寫入異常時自動觸發 `db.rollback()`，成功則 `db.commit()` [cite: 219, 223, 225, 227]。

### 3. 資料查詢與分析 (Data Query)
* [cite_start]系統能成功讀取並處理全體學生的完整成績資料（如測試範例中的 11 位學生） [cite: 126, 318]。
* [cite_start]自動提取資料庫數據，計算並印出各科 (國語、英語、數學、社會、自然) 的平均成績 [cite: 253, 307, 308, 309, 310, 311, 320]。

### 4. 成績修改 (Grade Update)
* [cite_start]支援對特定學生的特定科目進行分數單筆覆寫修正 (例如：將 Sophia 的中文成績更新為 99 分) [cite: 129, 340, 341, 342]。
* [cite_start]修改操作同樣受到 Try-Except 的安全機制防護 [cite: 343]。

### 5. CLI 互動式單筆登記 (Interactive CLI)
* [cite_start]提供終端機 (Terminal) 互動介面，系統會逐步提示輸入各項資訊 (姓名、性別及各科成績) 作為手動建檔的備案 [cite: 19, 23, 24, 26, 27, 28]。
* [cite_start]每筆資料輸入完畢後立即存入 MySQL 資料庫，並詢問是否繼續 (y/n) [cite: 21, 22]。

## 🚀 快速啟動指南 (Quick Start)
1. [cite_start]**環境部署**: 使用專案目錄下的 `docker-compose.yml` 啟動 MySQL 與 Adminer 容器 [cite: 50, 52]。
2. [cite_start]**套件安裝**: 於本機端終端機執行 `pip install mysqlclient` 安裝 Python 驅動套件 [cite: 103]。
3. [cite_start]**連線設定**: Python 腳本預設連線主機為 `localhost`，帳號 `root`，密碼 `123456`，資料庫名稱 `mydatabase` [cite: 142]。
