# skill-review

**用途**：在安裝任何第三方 Claude Code skill、GitHub 工具、或 CLI 工具之前，先進行安全審查。

## 觸發方式

當使用者說：
- 「幫我審查這個工具」
- 「我想裝 X，先幫我查一下」
- 「這個 GitHub repo 安全嗎？」
- 「/skill-review [GitHub URL 或 repo 名稱]」

## 審查流程

### 第一步：取得原始碼

使用 WebFetch 抓取 GitHub repo 的以下頁面：
1. `https://github.com/<owner>/<repo>` — 首頁、README、描述
2. `https://github.com/<owner>/<repo>/find/main` 或直接看 file tree
3. 重點目錄：`bin/`、`scripts/`、`src/`、`.claude/skills/`、`install.sh`

使用 `https://raw.githubusercontent.com/<owner>/<repo>/main/<file>` 取得原始檔案內容。

### 第二步：紅旗掃描（依優先順序）

**P0 — 立即停止，不要安裝：**
- 任何對外 HTTP 請求（`curl`、`fetch`、`axios`、`wget`）指向非 GitHub/npm 的域名
- 上傳或 POST 使用者資料到第三方伺服器
- 讀取並傳送 `~/.claude/`、`~/.ssh/`、`~/.env`、API key 相關檔案
- 安裝後台常駐程序（`launchd`、`systemd`、`cron`）

**P1 — 警告，需要使用者確認：**
- 包含 `telemetry`、`analytics`、`tracking`、`beacon`、`sync` 關鍵字的腳本或檔案
- 寫入 `*.jsonl` 或 `*.log` 檔案（尤其是記錄 skill 使用或對話內容）
- `install.sh` 在安裝時執行額外網路請求
- 需要 `OPENAI_API_KEY` 或其他 API key 且原因不明
- symlink 數量異常多（超過 10 個）

**P2 — 注意，但通常可接受：**
- 檢查更新（update check）機制 — 確認是否只讀不寫
- 使用 npm/pip/bun 安裝依賴 — 確認依賴本身無問題
- MCP server 設定 — 確認暴露的工具範圍合理

### 第三步：審查 install script

找到 `install.sh`、`setup.sh`、或 `Makefile` 的 install target，逐行分析：
- 它把檔案裝到哪裡？
- 它有沒有在背景啟動任何程序？
- 它有沒有修改 shell config（`.bashrc`、`.zshrc`）以外的系統設定？
- 它有沒有設定 cron job 或 launch agent？

### 第四步：審查 skill 檔案本身

若是 Claude Code skill（`.md` 檔案），確認：
- skill 的指令是否合理、有限
- 是否有要求 Claude 執行不尋常的 Bash 命令
- 是否有要求讀取敏感路徑

### 第五步：輸出報告

格式如下：

```
## 審查報告：<repo 名稱>

**整體評估**：✅ 安全 / ⚠️ 需確認 / ❌ 不建議安裝

### 基本資訊
- 作者：
- Stars / 最後更新：
- 授權條款：

### 紅旗項目
（列出發現的問題，若無則標示「未發現」）

### 安裝後會動到哪裡
（列出安裝腳本會建立的目錄、檔案、symlink、設定）

### 結論與建議
（具體說明是否安裝、有哪些條件）
```

## 注意事項

- 若 repo 是私有或無法存取，告知使用者並請他提供原始碼或安裝腳本內容
- 審查是靜態分析，無法保證 100% 完整；有疑慮就不裝
- 若工具需要 API key，確認 key 的用途和去向再決定
