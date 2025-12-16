# 貓咪闖關地圖

一個以一週為單位的任務闖關小工具，完成每日任務就能自動蓋章並收集貓咪貼紙。介面與文本以繁體中文呈現，適合親子一起使用。

## 特色
- **貼紙系統**：使用 `assets/Gemini_Generated_Image_5udqzj5udqzj5udq.png` 這張 10×10 的貓咪貼紙集合作為 sprite sheet，前端會自動生成 `.cat-<row>-<col>` 類別並套用到貼紙格；系統也會記錄 30 天內用過的貼紙，避免短期重複。 
- **任務與獎勵**：支援新增/刪除任務、點選完成狀態，以及點數或自訂獎勵；完成度會即時更新今日/本週的獎勵統計。
- **每週地圖視圖**：以 7 天地圖呈現當週進度，可透過日期選擇器或點擊地圖切換日期；完成當日任務會自動蓋章並收集貼紙到收藏列。
- **同步與儲存**：提供與 Google Apps Script API 的同步（查詢、新增、更新、刪除），同時透過 `localStorage` 保留每週任務、貼紙以及貼紙使用紀錄，離線時也能維持資料。

## 專案結構
- `index.html`：主要的 UI、任務流程與資料同步邏輯。
- `assets/style.css`：版面與貼紙 sprite 相關樣式。
- `assets/Gemini_Generated_Image_5udqzj5udqzj5udq.png`：10×10 貓咪貼紙 sprite sheet。

## 快速開始
1. 安裝相依：本專案不需要後端伺服器，只需一個靜態網站環境；若在本機，可用 Python 內建伺服器：
   ```bash
   python -m http.server 8000
   ```
2. 瀏覽器開啟 `http://localhost:8000`（或直接以檔案路徑開啟 `index.html`），即可開始使用。
3. 若要使用雲端同步功能，請確保 `index.html` 內的 `API_URL` 指向你可以存取的 Google Apps Script 端點。

## 操作提示
- 使用右側日期選擇器或點擊地圖的圓形關卡即可切換日期，版面會同步顯示對應的任務與獎勵。
- 任務打勾後若為當日，系統會自動蓋章並抽取一張未重複的貓咪貼紙；取消打勾會移除貼紙。
- 每週的任務與貼紙狀態會以週一為鍵儲存在瀏覽器 `localStorage`，重整頁面後仍會保留。

## 注意事項
- 若要自訂貼紙素材，只需替換 `assets` 內的貼紙 sprite 並更新 `CAT_SPRITE_ROWS`、`CAT_SPRITE_COLS` 與 `CAT_SPRITE_PATH` 設定。
- Google Apps Script 端點必須支援 GET/POST 並遵循程式碼中的參數約定，否則同步功能會失敗；失敗時資料仍會保留在本機。
