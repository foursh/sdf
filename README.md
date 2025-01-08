# 基本面爬蟲

## 簡介
此專案是一個股票財務數據查詢系統，能夠：
1. 爬取特定股票的財務報表（資產負債表、綜合損益表、現金流量表）。
2. 將爬取到的數據存儲至資料庫。
3. 根據財務指標進行計算與分析，提供分數和排名。
4. 通過 LINE Bot 與用戶互動，實現股票查詢和分析結果的即時回覆。

---

## 功能列表

1. **股票數據爬取**：
   - 從 [台灣證券交易所](https://mops.twse.com.tw/) 獲取指定股票的財務報表。
   - 支援多次爬取與錯誤重試機制。

2. **數據存儲與處理**：
   - 將爬取的報表存入資料庫模型 `Stock`。
   - 使用 Pandas 分析報表，計算重要財務指標（如毛利率、淨利率、EPS 等）。
   - 提供綜合分數和排名。

3. **LINE Bot 整合**：
   - 用戶輸入股票代碼即可查詢分析結果。
   - 自動回覆財務報表評分與排名。

4. **批量更新功能**：
   - 支援 CSV 文件批量更新股票數據。
   - 自動處理爬取失敗的股票代號。

---

## 系統架構

### 主要技術
- **後端框架**：Django
- **爬蟲**：`requests` + `BeautifulSoup`
- **數據處理**：Pandas
- **消息回覆**：LINE Messaging API

### 資料庫模型
1. **Stock**：
   - `stock_code`：股票代號
   - `B`：資產負債表 HTML
   - `P`：綜合損益表 HTML
   - `C`：現金流量表 HTML

2. **StockMetrics**：
   - 儲存計算出的財務指標數據及排名。

---

## 安裝與運行

### 環境需求
- Python 3.8 或以上
- pip 套件管理工具

### 安裝步驟

1. **克隆專案**：
   ```bash
   git clone https://github.com/your-repo/stock-finance-system.git
   cd stock-finance-system
   ```

2. **安裝依賴**：
   ```bash
   pip install -r requirements.txt
   ```

3. **設置環境變數**：
   創建 `.env` 文件，填入以下內容：
   ```env
   LINE_CHANNEL_ACCESS_TOKEN=your_line_bot_access_token
   LINE_CHANNEL_SECRET=your_line_bot_secret
   GROQ_API_KEY=your_groq_api_key
   ```

4. **遷移資料庫**：
   ```bash
   python manage.py migrate
   ```

5. **啟動伺服器**：
   ```bash
   python manage.py runserver
   ```

6. **啟用 Webhook**：
   配置 LINE Messaging API Webhook 指向 `http://<your-server-domain>/callback/`。

---

## 使用說明

### 透過 LINE Bot 查詢股票
1. **輸入股票代碼**：用戶直接在 LINE Bot 中輸入股票代碼，例如 `2330`。
2. **回覆結果**：系統將回覆財務報表分析分數與排名。

### 網頁查詢
1. 瀏覽 `http://127.0.0.1:8000/query_report/`。
2. 輸入股票代號進行查詢，瀏覽報表與計算結果。

---

## 文件結構

```plaintext
stock-finance-system/
├── manage.py             # Django 管理指令入口
├── app/
│   ├── models.py         # 資料庫模型
│   ├── views.py          # 主邏輯控制
│   ├── templates/        # HTML 模板文件
│   └── static/           # 靜態文件
├── requirements.txt      # 相依套件清單
├── README.md             # 專案說明文件
└── .env.example          # 範例環境變數文件
```

---

## 進一步開發
### 新增功能
- 股票數據可視化（例如歷史股價走勢圖）。
- 多語言支援（繁體中文、英文）。

### 測試
- 編寫單元測試以覆蓋關鍵功能（爬蟲、數據處理、API 整合）。

---

## 貢獻指南
1. Fork 此專案。
2. 創建分支並進行修改。
3. 提交 Pull Request。

---

## 聯絡方式
- 作者：Your Name
- 電子郵件：your_email@example.com

---

## 授權
本專案採用 MIT 授權，詳見 [LICENSE](LICENSE)。