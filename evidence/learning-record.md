# Learning Record / 學習紀錄

- **學期 / 單元：** NDHU Agent Lab · Week 05
- **組別：** G-W05
- **工具：** Antigravity / Gemini 3.8 Flash (High)
- **路線：** individual 個人
- **完成任務：**
  - Task A: 整理社團檔案 (`A: organize club files`)
  - Task B: 課間挑選器 (`B v1: activity picker`, `B v2: add match count badge and avoid consecutive duplicates`)
  - Task C: 社團器材資料清理 (`C: normalize equipment data`)
  - Task D: 計畫審查與退回 (`D: rejection`)
  - 實作成果紀錄 (`record: learning record and screenshots`)

---

## 歷程總結

1. **Task A (整理社團檔案):**
   - 盤點 12 個文字檔，精確辨識 2 組完全重複檔案（`announcement` 與 `equipment` 系列）及 2 個不同討論草案（`proposal_final` 與 `proposal_final2`）。
   - 保留全部 12 個原檔，輸出 12 個分類副本至 5 個分類資料夾，無任何破壞性操作。
   - 產出 `manifest.json` 與 `report.md`。

2. **Task B (課間活動挑選器):**
   - 建立離線單頁 `index.html`，支援地點、時間、強度三條件篩選。
   - 支援最近 5 次歷史紀錄、重設篩選、中英雙語切換。
   - 第二版優化：新增符合條件總筆數顯示徽章、連續抽選防重複機制、切換淡入動畫。

3. **Task C (器材記錄資料清理):**
   - 原始 10 列中過濾 1 列全空無效列，保留 9 筆有效列（保留 `source_row`）。
   - 統一狀態為 `available`、`borrowed`，非標準狀態（`待盤點`）轉換為 `unknown`。
   - 數量異常（空字串 `""` 與負數 `-1`）原樣保留不補 0，不猜測。
   - 保留重複編號 `EQ01` 與 `EQ02`，並於報告中明確指出 `EQ02` 數量衝突（2 vs 3）。
   - 產出 `normalized.json` 與 `issues.md`。

4. **Task D (審查與退回):**
   - 針對未經授權存取 Downloads、未經確認刪檔、猜測補值與自動外傳等四大高風險動作提出具體審查與退回依據。
   - 提出非破壞、保留不確定性與封閉執行的替代方案。

5. **安全與判斷心得：**
   - AI Agent 的工作必須嚴格限定範圍。
   - 凡涉及「刪除」、「覆蓋」與「公開」皆須視為高風險動作，先提計畫經人類確認才執行。
