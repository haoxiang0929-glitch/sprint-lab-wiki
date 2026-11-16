Markdown
# AGENTS.md — Sprint Lab 短跑與運動科學知識庫開發規範

## 1. 專案目的 (Project Purpose)
本專案為個人「短跑訓練與運動科學筆記庫（Sprint Lab Wiki）」，旨在系統化整理 100m/200m 短跑技術拆解、生物力學數據、肌力體能週期安排及訓練復盤。
**核心目標**：建立高度模組化的靜態網頁架構，讓 AI 助手在未來只需接收到「新增一篇筆記」的指令與草稿內容時，便能全自動生成符合規範的新 HTML 頁面，並同步更新首頁索引。

---

## 2. 整體視覺與技術風格 (Design & Tech Stack)
- **技術棧**：純 HTML5 + Tailwind CSS (透過 CDN 載入) + Vanilla JavaScript。**嚴禁**引入 React、Vue 或任何需要 Build Step（如 Webpack/Vite）的框架，確保 GitHub Pages 零設定直接部署。
- **視覺主題**：田徑賽道極簡運動風（Dark Track Theme）。
  - 主背景色：`#0f172a` (`slate-900`)
  - 卡片與區塊背景：`#1e293b` (`slate-800`)，邊框 `border-slate-700`
  - 強調色（田徑跑道橘紅）：`#f97316` (`orange-500`)
  - 數據/科學高亮色：`#38bdf8` (`sky-400`)
  - 文字主色：`#f8fafc` (`slate-50`)，次要說明文字：`#94a3b8` (`slate-400`)
- **字體**：無襯線體為主，數據與配速/秒數一律使用等寬字體 (`font-mono`)。

---

## 3. 檔案命名與目錄結構 (File Naming & Structure)
所有檔案皆置於根目錄（扁平化結構，避免相對路徑錯誤）：
- `AGENTS.md`：本專案最高指導原則。
- `index.html`：主首頁，包含網站標頭、分類篩選按鈕、以及所有筆記的卡片列表。
- `post-[英文短網址].html`：單篇筆記頁面。
  - **命名規則**：必須以 `post-` 開頭，全小寫英文，單字間以連字號 `-` 分隔（例如：`post-start.html`、`post-max-velocity.html`、`post-hip-mobility.html`）。

---

## 4. 頁面結構規範 (Page Architecture)

### A. 首頁 (`index.html`)
1. **Header**：顯示網站名稱「SPRINT LAB // 短跑運動科學筆記」與副標題。
2. **Filter Bar**：提供分類篩選標籤（`全部`、`技術力學`、`肌力體能`、`訓練復盤`）。
3. **Article Grid**：響應式卡片網格 (`grid-cols-1 md:grid-cols-2 gap-6`)。每張卡片必須包含 `data-category` 屬性以支援 JS 篩選。

### B. 單篇筆記頁 (`post-*.html`)
1. **Top Nav**：左上角固定提供「← 返回筆記列表 (`index.html`)」連結。
2. **Article Header**：分類標籤（Badge）、文章標題 (`text-3xl font-bold`)、發布日期與預估閱讀時間。
3. **Key Metrics Box (核心數據摘要區)**：每篇文章開頭**必須**包含一個 3 欄數據卡片 (`grid-cols-3`)，提煉該主題最關鍵的 3 個量化指標或核心參數。
4. **Main Content**：使用清晰的 `<h2>` 段落標題、條列式重點，以及「常見錯誤 vs. 正確動作」對照區塊。
5. **Footer**：統一版權與返回首頁按鈕。

---

## 5. AI 新增或修改內容的標準作業程序 (SOP for AI)
當使用者要求「新增一篇關於 [主題] 的筆記」時，AI **必須**嚴格執行以下 3 個步驟，缺一不可：

1. **建立新頁面**：
   - 依據規則命名為 `post-[slug].html`。
   - 完全複製 `post-start.html` 的 `<head>`、Tailwind 設定與版面骨架。
   - 將內容填入，並確保包含 **Key Metrics Box (3 個核心量化指標)**。
2. **同步更新 `index.html`**：
   - 在 `index.html` 的 `<div id="posts-grid">` 最上方插入新文章的卡片 HTML。
   - 卡片的 `href` 必須正確指向新建的 `post-[slug].html`。
   - 卡片的 `data-category` 必須精準對應現有分類之一（`技術力學`、`肌力體能`、`訓練復盤`）。
3. **自我檢查**：
   - 確認所有連結皆為相對路徑（不加開頭 `/`），確保在 GitHub Pages 子路徑下可正常跳轉。
   - 維持繁體中文（台灣田徑與運動科學慣用語，如：起跑架、步頻、步幅、觸地時間、後側鏈）。
