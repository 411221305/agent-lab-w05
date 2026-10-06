# My lab evidence / 我的實作紀錄

Use a group code, not real names or student IDs in shared files. / 共用檔只寫組別代碼，不寫姓名或學號。

- Group code / 組別：G-W05
- Tool / 工具：Antigravity (Gemini 3.8 Flash High)
- Route / 路線：individual 個人
- Tasks completed / 完成題目：A, B, D
- Material / 素材：NDHU classroom tasks 東華課堂版
- For original-pack work: task number, author/source link and version / 原版實作：題號、作者來源連結與版本：無（使用東華課堂版）
- My role and what I checked / 我的角色與實際檢查：負責提示詞提供、執行前計畫審核、成果檔案與雜湊比對驗證、活動挑選器功能與邊界測試、不合理計畫之審查與退回。

## Scope and plan / 範圍與計畫

Allowed input and output folders / 可讀取與輸出的資料夾：
- Task A: 讀取 `practice/01-club-files/input/`，僅輸出至 `practice/01-club-files/output/`
- Task B: 讀取 `practice/02-campus-picker/activities.json`，僅輸出至 `practice/02-campus-picker/output/index.html`
- Task D: 讀取 `practice/04-review/bad-plan.txt`，僅輸出至 `practice/04-review/my-rejection.md`

What I asked for / 原始需求：
- Task A: 盤點整理 12 個文字檔，分類複製到 output，保留所有原檔與不同草案版本，產出 manifest.json 與 report.md。
- Task B: 製作單頁離線校園課間活動挑選器，依地點、時間、強度進行篩選抽選，具備歷史紀錄（最近5筆）、中英雙語切換、重設篩選功能。
- Task D: 審查刻意寫錯的模擬計畫，提出具體問題並寫出退回與替代方案。

What I checked before execution / 動手前我檢查了什麼：
- 確認 AI 助理工作目錄是否正確限制在本題資料夾內，未擴及其他個人目錄。
- 確認計畫中是否明確承諾「不刪除原檔、不覆蓋不同版本、不自動猜測或公開資料」。
- 在確認計畫無破壞性動作後，才發出「執行」指令。

## Tests actually performed / 我真的做過的測試

| Test / 測試 | Expected / 預期 | Observed / 實際 | Evidence / 證據 |
|---|---|---|---|
| 1. Task A 檔案雜湊與數量比對 | 12 個原檔皆在，output 有 12 個分類副本，MD5 雜湊 100% 一致 | 透過比對腳本檢驗，12 筆原檔與副本雜湊完全吻合，manifest.json 為 12 筆陣列 | `practice/01-club-files/output/manifest.json`、`report.md` |
| 2. Task B 無符合條件邊界測試（室外／15分鐘／中強度） | 無任何符合活動，顯示「沒有符合條件的活動」，不偷放寬條件且不寫入歷史 | 畫面正確顯示無符合活動訊息，歷史紀錄筆數未增加 | `practice/02-campus-picker/output/index.html` |
| 3. Task B 唯一解測試（室外／30分鐘／中強度） | 僅 A09 符合條件，每次抽選結果皆為 A09 | 連續點擊抽選皆穩定顯示 A09 | `practice/02-campus-picker/output/index.html` |
| 4. Task B 歷史上限與重設測試（抽6次 + 重設篩選） | 歷史上限為 5 筆（最新在前）；重設篩選器為預設值但歷史仍保留 | 歷史紀錄僅保留最新 5 筆；點擊重設篩選後條件還原為預設，歷史紀錄完整存在 | `practice/02-campus-picker/output/index.html` |

## One revision / 一次修改

Before / 原來的情況：
第一版 (v1) 抽選結果未顯示目前條件下的候選活動總筆數，使用者無法得知有多少活動符合；且若候選數大於等於 2 筆時，可能連點抽到同一項活動，容易讓使用者誤以為點擊沒反應。

Request / 我提出的修改：
1. 在結果卡片增加「符合條件活動共 N 項 / N matching activities」提示徽章。
2. 當符合條件數 $\ge 2$ 筆時，加入「連續抽選不重複」機制，排除剛才抽中的活動。
3. 加入切換淡入動畫效果以提供點擊回饋。

After and retest / 修改後與重測結果：
修改後進行測試：選擇「室外／30分鐘／中強度」時正確標示「符合條件活動共 1 項」；選擇「室內／15分鐘／低強度」時標示「共 4 項」，連續多次點擊「幫我選」均順暢切換不同項目，未發生連續兩次抽到相同 ID 的狀況。

New requirement or defect? / 新需求還是原規格未做到？
屬於新需求（使用者體驗優化），原規格僅要求基本隨機抽選，增加候選筆數與防連抽為提升互動體驗之強化功能。

## One rejection / 一次退回

Which action I reject and why / 退回哪個動作、為什麼：
退回 `bad-plan.txt` 中的四大危險操作：
1. 「整理整個 Downloads 資料夾」：權限失控，威脅使用者非專案檔案安全。
2. 「刪除重複檔，把 final2 當作最新版」：刪除不可逆，且 final/final2 僅為不同草案版本，隨意刪除會遺失重要資料。
3. 「找不到資料補合理值」：擅自猜測或造假數據，違反資料真實性原則。
4. 「自動公開成果」：未經人類授權自動外傳，存在隱私與未定稿內容外洩風險。

An acceptable alternative / 可以怎麼改：
嚴格限定在指定的專案資料夾作業；所有原檔與版本完整保留於 output；缺漏資料如實標註於問題報告；本機封閉產出，未獲明確授權不進行任何發布動作。

## Still unverified / 還沒驗證

What I cannot claim is complete / 哪些事不能說已完成：
1. 隨機抽選演算法的長期機率公平性尚未經過大樣本統計驗證。
2. 重複檔案（如通知副本與器材備份）之後續去重與刪除決策，仍待真實社團幹部開會確認。
