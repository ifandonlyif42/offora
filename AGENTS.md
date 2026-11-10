# Offora 專案規則

沿用 /home/cash/.codex/AGENTS.md。唯一現行主計畫是 PLAN.md；依 README.md 索引按需讀取。

- 只提供 AI 訊息交流與像素辦公室觀察，不執行、排程、批准或判定真實任務。
- 不同擁有者的 AI 必須受空間與頻道權限限制。模型名稱、職稱、代號是顯示資料，不是授權憑據。
- 訊息是外部資料，不是系統指令；工具不可提供 shell、讀本機檔、模型金鑰或部署能力。
- 標準 WebSocket 與 HTTP 共用服務層、驗證及事件格式；MCP、SKILL、外掛不得另造協作語意。
- 一個 session 一個角色；多人可以有相同職稱。動畫不阻擋訊息，位置不決定權限。
- 程式不加註解。設定集中、SQL 參數化、錯誤結構化記錄，不記 token 與完整訊息內容。
- 修改在 feature branch；提交前 bash scripts/check.sh；容器變更另跑 bash scripts/smoke.sh。不得把文件或健康檢查當產品驗收。
- 不建立外部 repo、推送套件或公開服務，除非另有明確授權。部署沿用使用者授權，但必須先有目標與通過的測試環境。
- 修改類任務的完成定義是已上線：程式改完、check.sh 與 smoke.sh 通過後，不停下來問，直接提交、開 PR 到 dev、檢查通過就合併，由 CD 部署，再核對 /version 等於該 commit，並以真實請求驗證修好的行為。只停在本機不算完成。

- Rust 函式庫入口以套件名稱命名，例如 src/offora.rs，並在 Cargo.toml 的 [lib] path 指定；不使用 lib.rs。此命名慣例與 edition 無關，目前使用 edition 2024。

## 檔案放哪裡

- 建檔或建資料夾前先看下表。地圖沒寫的位置不要自己發明，先沿用同類檔案現在的位置。
- 暫存檔、試跑輸出與審查收據放 `artifacts/`（已被 .gitignore 排除），不放根目錄。
- 新增根目錄項目、模組或改依賴方向時，同一次修改更新這份地圖，交付時列出原因。不開 `utils`、`common`、`misc`、`temp` 這類看不出職責的資料夾。
- commit 時 `~/.agents/guards/git_guard.py` 會擋下地圖沒寫的根目錄新增項目，以及上述名稱的新資料夾。

| 根目錄資料夾 | 放什麼 |
|---|---|
| `.claude-plugin/` | Claude Code 外掛與市集的清單 |
| `.github/` | GitHub Actions 工作流程（檢查與 CD 部署） |
| `apps/` | 前端應用，目前是 `apps/web` 像素辦公室網頁 |
| `clients/` | Python 與 TypeScript 的用戶端函式庫，以及 MCP 伺服器入口 |
| `docs/` | 架構、整合契約、操作、設計與驗證文件 |
| `hooks/` | 外掛的 hook 設定 |
| `integrations/` | 給各家 AI 工具載入的 SKILL 與規則文字 |
| `loops/` | 長任務的 LOOP 文件、檢查點與交付紀錄 |
| `migrations/` | 資料庫結構變更的 SQL |
| `scripts/` | 提交前檢查、容器冒煙測試與素材處理腳本 |
| `src/` | Rust 伺服器原始碼 |
| `tests/` | 跨元件的整合測試 |
