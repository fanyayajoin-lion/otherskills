# otherskills — Claude Code 知識工作區

個人 Claude Code 配置、Skills 與最佳實踐筆記。

## 已安裝

| 工具 | 版本 | 說明 |
|------|------|------|
| gbrain | 0.26.0 | AI agent 記憶系統（PGLite 向量庫） |

詳見 [gbrain-install.md](./gbrain-install.md)

## 知識庫

### Claude Code 最佳實踐（2026-05-16）

來源：[完整研究報告](https://github.com/zeuikli/claude-code-workspace/blob/main/docs/2026-05-16-claude-code-best-practices.md)

九大面向核心要點：

1. **CLAUDE.md**：最多 200 行，超過遵從率從 76% 降到 52%
2. **Hooks**：PreToolUse 防危險操作 / PostToolUse 自動格式化，exit 2 = 完全阻擋
3. **Prompt Caching**：system prompt 完全靜態，動態資訊用 `<system-reminder>` 注入 message
4. **Subagent**：讀 ≥10 檔 / >20 tool calls / 可拆 ≥3 子任務 → 委派；最多同時 4 個
5. **Skill**：≤150 行，API 最多載入 8 個，高風險操作給低自由度
6. **MCP**：`defer_loading: true` 節省 85% tool schema tokens
7. **安全**：四層防禦（Permission → Sandbox → Proxy → Container），Agent 不直接持有 API Key
8. **Routines**：三種觸發（定時 / API / GitHub Event），prompt 需完全自給自足
9. **成本**：Haiku + Opus Advisor 節省 85%；CJK 禁用 LLMLingua

### Context 狀態速查

| 使用率 | 動作 |
|--------|------|
| 0–70% | 正常 |
| 70–85% | `/compact <hint>` |
| 85–95% | 完成當前任務 |
| 95%+ | `/clear` 開新 session |

## Session 記錄

### 2026-06-23
- 讀取並摘要 CC 最佳實踐完整研究報告（9 面向 + Appendix）
- 建立 CC 顧問知識框架，整理可延伸諮詢的問題清單
- 建立 CLAUDE.md 與本 README
