# 專案進度交接文件

**Repository**：`fanyayajoin-lion/otherskills`
**工作分支**：`claude/consultative-sales-framework-QzTgF`
**最後更新**：2026-05-25

---

## 專案目標

將「TUP 顧問式銷售法」課程內容與「LIFO 個人行為風格分析」問卷，轉化為可在 Claude Code 中直接呼叫的 Skill 工具組。

---

## 已完成項目

### Skill 1：`consultative-sales`
- **路徑**：`skills/consultative-sales/SKILL.md`
- **來源**：`e4441ebc-__________.docx`（TUP 課程逐字稿）
- **功能**：顧問式銷售法完整流程教練
- **包含內容**：
  - 銷售三問框架
  - 完整銷售流程（尋找顧客 → 確認需求 → 提供滿意方案 → 疑義處理 → 成交）
  - 確認需求技術（改進／減低／維持 + 開放式／封閉式問法）
  - 特色 vs. 效益轉換公式
  - 物超所值心理公式（顧客所得 ÷ 顧客所付 > 1）
  - 顧客 → 客戶 → 轉介紹中心轉化路徑
  - 四段話術模板（開場／需求確認／方案說明／促成）
  - 底層心法（布局思維、情理法、六字真經）

### Skill 2：`customer-profiling`
- **路徑**：`skills/customer-profiling/SKILL.md`
- **來源**：`02e8f54d-______2018___02________.ppt`（LIFO 問卷簡測表，OLE 格式，以 `olefile` 解析提取）
- **功能**：客群行為風格診斷工具
- **包含內容**：
  - LIFO 完整 18 題問卷（原始題目）
  - 計分方式（A=SG、B=CT、C=CH、D=AD，四欄總和必須等於 90）
  - 四種風格完整描述：
    - 卓越 SG（無尾熊／支持者）
    - 行動 CT（老虎／掌控者）
    - 理性 CH（貓頭鷹／持穩者）
    - 和諧 AD（孔雀／順應者）
  - 每種風格：核心取向、優點與過當對照表、銷售溝通策略、雷區
  - 觀察模式（無法測驗時，用日常行為線索快速推斷）
  - 標準輸出報告格式
  - 與顧問式銷售四個環節的整合對照表
  - 快速風格識別備忘卡

### 部署狀態
- 兩個 Skill 均已 commit 並 push 至 `claude/consultative-sales-framework-QzTgF`
- 已同步複製至 `/root/.claude/skills/`，可直接以 `/customer-profiling` 和 `/consultative-sales` 呼叫

---

## 待辦事項（尚未開始）

> 由下一位 CC 接手時，與用戶確認後繼續執行。

- [ ] 兩個 Skill 實際使用測試與微調
- [ ] 根據用戶回饋修訂話術範本
- [ ] 其他用戶提出的新需求

---

## 目錄結構

```
otherskills/
├── PROGRESS.md                         ← 本檔案（進度交接）
├── skills/
│   ├── consultative-sales/
│   │   └── SKILL.md                    ← 顧問式銷售法 Skill
│   └── customer-profiling/
│       └── SKILL.md                    ← LIFO 客群診斷 Skill
└── gbrain-install.md
```

---

## 原始素材位置

| 檔案 | 說明 |
|------|------|
| `/root/.claude/uploads/.../e4441ebc-__________.docx` | TUP 顧問式銷售法課程逐字稿 |
| `/root/.claude/uploads/.../02e8f54d-...__.ppt` | LIFO 個人行為風格分析簡測表（OLE 格式） |
