# CT小舖 V93

本版針對「Slash 指令偶發無法使用／權限不足」做穩定性修正。

- 管理員判斷改為 Discord 實際 Member 權限優先，再檢查設定的管理員身分組。
- 相容既有管理角色名稱：管理員、店長、店長👑、闆闆👑。
- 指令錯誤會區分「使用者權限不足」與「機器人被 Discord 拒絕」。
- 啟動時輸出機器人 Administrator／Manage Guild／Manage Channels／Manage Messages／View Channel／Send Messages 權限，方便 Railway Log 定位。
- V82 的 `/改名工單` 全部在 Slash 輸入欄操作保留。
- V78～V82 已完成的工單結單、付款圖片檢查、舊指令清理等邏輯保留。


## V84 變更
- 自動算價不偵測帶 M 的額度（例如 50M、100M、200M）。
- /改名工單新增 200M。
- /改名工單 的狀態與額度改為依「幣號／代肝」動態分流，不再共用選項。
- 改名工單維持全部在 Slash 指令輸入欄完成。


## V91 付款圖片確認規則
- 店長只有在訂單已偵測到客人付款成功明細圖片後，才會看到「💰 確認付款」按鈕。
- 沒有圖片時，即使舊訊息仍存在確認按鈕，點擊也會再次檢查並拒絕確認。
- 圖片偵測不再依賴 `TICKET_CHANNEL_IDS` 快取。
- 支援 PNG / JPG / JPEG / WEBP / GIF / BMP / HEIC / HEIF。
- 圖片可以在客人按「完成付款」後上傳，也能在按鈕前先上傳；店長確認前都會檢查。
- 客人按「💳 完成付款」後會收到：`✅ 成功提交付款通知，請等待店長`

# V92 付款圖片確認修正
- 完整保留 4 檔：bot.py、Procfile、README.md、requirements.txt。
- 店長只有在訂單已有付款成功明細圖片時，才能按「💰 確認付款」。
- 客人可以先上傳付款圖片，再按「💳 完成付款」；按下後會立即回掃工單歷史並綁定圖片。
- 客人也可以先按「💳 完成付款」，再上傳付款圖片。
- 圖片支援 png、jpg、jpeg、webp、gif、bmp、heic、heif 及 image/*。


## V93 修正
- `/改名工單` 進入指令後立即 ACK/defer，再執行權限、SQLite 與 Discord API 操作，避免超過 Discord 3 秒 Interaction 回應期限造成 `Unknown interaction (10062)`。
- 改名工單所有錯誤回覆統一使用 followup。
- 補回 `migrate_legacy_ticket_names()`，修正啟動時 `[LEGACY_MIGRATE] ... NameError`。
- 保留付款圖片才能確認付款的 V92 規則與四檔完整包結構。
