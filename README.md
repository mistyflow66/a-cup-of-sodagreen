# 💚 a-cup-of-sodagreen

**[網站連結](https://mistyflow66.github.io/a-cup-of-sodagreen/)**

> A digital Sodagreen Oracle. Click to receive a random lyric for daily guidance, paired with a timestamped YouTube MV of the corresponding song.

---

## ⚙️ 系統運作核心邏輯 (System Logic)

這個專案是一個由 **Google 試算表** 驅動的隨機歌詞抽取器，結合雲端後端服務 (Apps Script) 和靜態網頁 (GitHub Pages) 來實現數據的動態展示。

### 1. 核心元件架構

整個系統的數據流可視為一條穩定管道，由以下三個元件構成：

* **數據庫 (Google Sheets):** 儲存所有歌詞、歌名、網址等資料，作為唯一的數據源。
* **後端 API (Apps Script):** 將私有的 Google 試算表數據轉換成公開、安全的 JSON 格式 API。
* **前端 (GitHub Pages):** 負責用戶介面、數據解析與多媒體控制。

### 2. Apps Script 數據處理與穩定性

後端服務是系統運作的關鍵，它負責將試算表數據轉換為前端可讀的格式：

* **穩定連線機制：** 程式碼使用 **試算表 ID (`SpreadsheetApp.openById`)** 進行連線，確保權限穩定，避免 Apps Script 服務意外中斷。
* **數據格式化：** Apps Script 讀取試算表後，將中文標頭（如：「歌詞」、「網址」）作為 **JSON 物件的鍵 (Key)** 輸出。
* **錯誤處理：** 若連線失敗，Apps Script 會返回一個空的 JSON 陣列 (`[]`)，防止網站崩潰。

### 3. 前端 MV 嵌入與優化

前端 JavaScript (在 `index.html` 中) 負責處理影片播放的各種細節：

* **ID 提取：** 使用強化函式從各種 YouTube 網址中精準提取 11 位元的影片 ID。
* **播放穩定性修正：** 影片嵌入網址強制使用 **`https://www.youtube-nocookie.com/embed/`** 網域，解決了常見的 **Mixed Content 錯誤** 及嵌入權限衝突問題。
* **秒數定位：** 根據數據中的 `起始秒數（選填）` 欄位，在嵌入網址中加入 `&start=X` 參數，實現影片從指定時間點開始播放。
* **容錯機制：** 當數據中網址為空或無效時，程式碼會自動隱藏播放器，僅顯示歌詞。

---

## 📢 著作權與免責聲明 (Disclaimer & Copyright)

本專案「a-cup-of-sodagreen」是一個由蘇打綠樂團歌迷建立的**個人非營利分享專案**，目的僅為娛樂、交流與技術展示，不作任何商業用途。

### ⚖️ 著作權歸屬

* **歌詞及音樂內容：** 本專案中使用的所有 **歌詞、音樂內容、音訊及影像（YouTube 影片）** 之著作權及相關權利，均完全歸屬於 **蘇打綠樂團（Sodagreen）及其所屬唱片公司**。
* **投稿資料：** 投稿者提供的**選段、時間點及歌曲資訊**等數據，視為同意收錄於本站。本站僅做整理與展示，不主張任何對原始歌詞的權利。

### 🚫 免責聲明

* **非官方性：** 本網站**並非蘇打綠樂團官方網站或其附屬機構**。
* **非侵權意圖：** 本專案的使用方式旨在教育、技術展示和粉絲交流，**絕無意圖侵犯任何版權或著作權**。
* **內容授權：** 投稿者提交內容即視同**同意**其內容可收錄於本站，用於**非營利性**的整理和展示。
* **問題與聯繫：** 如版權持有者或相關人士對內容有任何疑慮，請立即聯繫本專案維護者，我們將迅速處理並進行修改或撤除相關內容。

---

### 🛠️ 參與及回饋

如果您發現任何歌詞錯誤，或有**更多喜歡的歌詞想加入資料庫**：

* **歌詞投稿表單：**
    [![投稿表單](https://img.shields.io/badge/Google%20Forms-%E6%AD%8C%E8%A9%9E%E6%8A%95%E7%A8%BF-4CAF50?style=for-the-badge&logo=google-forms)](https://docs.google.com/forms/d/e/1FAIpQLScvXqQpys7MC3jdPW60TcvJQpyDJ8XHzQfWWWsvr8f26Tlh1Q/viewform?usp=sf_link)
