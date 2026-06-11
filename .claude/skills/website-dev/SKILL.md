---
name: website-dev
description: Nick 個人網站(Vue 3 + Tailwind CSS 4 + Vite)的開發規範與設計系統。凡是要對這個網站做任何開發工作 — 新增區塊(section)、修改元件、加作品到 Projects、調整樣式、更新內容文案、改 NavBar 連結 — 都務必先使用這個 skill,即使只是小改動,因為網站有一套嚴格的視覺設計系統(深色底、violet/pink 漸層、白色透明度階層)和元件結構慣例,不照規範寫出來的東西會明顯格格不入。
---

# Nick 個人網站開發規範

這是一個單頁式個人作品集網站。所有改動的最高原則:**新東西看起來必須像是原本就存在於這個網站** — 訪客不該能分辨哪個區塊是後來加的。

## 技術棧與指令

- Vue 3.5(一律用 `<script setup>`,不用 Options API)
- Tailwind CSS 4(透過 `@tailwindcss/vite` plugin,**沒有** tailwind.config 檔;用 CSS-first 的 v4 語法)
- Vite 8,開發伺服器固定在 port 5175;路徑別名 `@` → `src/`
- shadcn-vue(JavaScript 模式、reka-ui 底層、lucide 圖示)— UI 元件的首選來源,見下方「UI 元件」一節
- 純前端、無路由、無狀態管理庫 — 不要引入其他新依賴,除非使用者明確要求

```bash
npm run dev      # 開發(http://localhost:5175)
npm run build    # 建置
```

## 專案結構

```
src/
├── App.vue              # 只負責組裝:NavBar → main(各 section)→ FooterBar
├── main.js
├── style.css            # @import "tailwindcss" + 極少量全域樣式
├── components/          # 自寫元件,扁平結構
│   ├── ui/              # shadcn-vue 產生的元件(button、input、card…),勿手動大改
│   ├── NavBar.vue
│   ├── HeroSection.vue
│   ├── ProjectsSection.vue
│   ├── ContactSection.vue
│   └── FooterBar.vue
├── lib/utils.js         # shadcn-vue 的 cn() 工具
└── assets/
```

### 新增一個區塊(section)的標準流程

1. 在 `src/components/` 建立 `XxxSection.vue`(PascalCase,區塊一律以 `Section` 結尾)
2. 在 `App.vue` import 並插入 `<main>` 內正確的位置
3. 若這個區塊應出現在導覽列,在 `NavBar.vue` 的 `links` 陣列加一筆 `{ href: '#xxx', label: 'Xxx' }`(label 用簡短英文)

## 設計系統(最重要的部分)

Tailwind CSS 4 語法注意:漸層用 `bg-linear-to-r`/`bg-linear-to-b`(不是 v3 的 `bg-gradient-to-r`);任意值如 `blur-[120px]`、`bg-size-[72px_72px]` 照舊可用。

### 色彩

- 背景:純黑 `bg-black` 與 `bg-neutral-950` 交替使用,讓相鄰區塊有層次
- 強調色:violet 為主、pink 為輔。漸層文字/按鈕用 `from-violet-400 to-pink-400`(文字)或 `from-violet-600 to-pink-600`(按鈕底)
- 文字階層全部用白色 + 透明度,**不要用灰色色票**:
  - 主標題 `text-white`
  - 副文字 `text-white/70` 或 `text-white/50`
  - 弱化資訊 `text-white/40`、`text-white/30`
  - 極弱(footer)`text-white/20`
- 邊框:`border-white/10`,hover 時提升為 `border-violet-500/50` 或 `border-white/50`

### 每個 section 的固定骨架

```html
<section id="xxx" class="py-32 px-6 bg-neutral-950">  <!-- 或 bg-black -->
  <div class="max-w-6xl mx-auto">                      <!-- 窄內容用 max-w-xl/3xl -->
    <!-- 標題區:violet 小眉標 + 大標 -->
    <div class="mb-16">
      <p class="text-violet-400 text-xs tracking-widest uppercase mb-3">English Eyebrow</p>
      <h2 class="text-4xl font-bold text-white">中文標題</h2>
    </div>
    <!-- 內容 -->
  </div>
</section>
```

### 常用元件模式

- **卡片**:`bg-white/5 border border-white/10 rounded-2xl p-7`,hover 用 `hover:border-violet-500/50 hover:bg-white/[0.07] transition-all duration-300`,搭配 `group` 做內部元素的 hover 連動
- **標籤(pill)**:`text-xs px-3 py-1 rounded-full bg-white/5 border border-white/10 text-white/60`
- **主要按鈕**:白底黑字 `px-8 py-3.5 bg-white text-black rounded-full font-semibold hover:bg-white/90 hover:scale-105` 或漸層 `bg-linear-to-r from-violet-600 to-pink-600 rounded-xl`
- **次要按鈕**:描邊 `border border-white/20 text-white rounded-full hover:border-white/50 hover:bg-white/5`
- **背景光暈(glow)**:大區塊可加 `absolute ... bg-violet-600/10 rounded-full blur-[100px] pointer-events-none`,記得父層 `relative overflow-hidden`
- **輸入框**:`bg-white/5 border border-white/10 rounded-xl text-white placeholder-white/20 focus:border-violet-500/60`
- 所有互動元素都要有 `transition-all duration-300`(或 `transition-colors duration-200/300`)

### 文案語言慣例

UI 是中英混排,有固定分工:

- 眉標(eyebrow)、badge、NavBar 連結、小型 UI 標籤 → **英文大寫間距字**(`tracking-widest uppercase`),如 "Portfolio"、"Get in touch"
- 區塊主標題、敘述文字、按鈕文字 → **繁體中文**,如「精選作品」「聯絡我」「查看作品」

## UI 元件(shadcn-vue)

需要互動性元件(按鈕、表單、對話框、下拉選單、tooltip 等)時,優先用 shadcn-vue,不要從零手刻:

- 已安裝:button、input、textarea、label、badge、card。缺什麼就先裝:`npx shadcn-vue@latest add <name>`(專案是 JavaScript 模式,CLI 會自動產生 .js/.vue)
- **元件全部自動匯入**(`unplugin-vue-components`,掃描 `src/components/` 全目錄):template 直接寫 `<Button>`、`<NavBar />` 即可,**不要**手寫元件的 import 陳述式(寫了也能動,但違反專案慣例)。僅限元件;`ref`、`cn()` 等函式仍需手動 import
- 主題已調校:`src/style.css` 的 `:root` CSS 變數已對應網站設計系統(`--background` 純黑、`--primary` 白、`--ring` violet、`--border` white/10、`--radius` 0.75rem)。**網站是永久深色,不使用 `.dark` class 切換**
- 元件預設樣式已大致貼合網站,但仍可用 class 微調(如 `rounded-full`、漸層底);客製時遵循上方設計系統
- 注意:執行 shadcn-vue CLI 後檢查 `src/style.css` 是否被塞回 Google Fonts 的 Geist `@import` — 網站字體是 system-ui,該行要移除
- 純展示性的卡片/標籤若既有 section 已有手刻樣式(如 ProjectsSection 的卡片),維持原有寫法即可,不必改用 shadcn-vue

## 程式碼慣例

- 資料(作品清單、連結、技能等)直接寫成 `<script setup>` 內的 `const` 陣列物件,不抽離成 JSON 或獨立檔案 — 範例見 `ProjectsSection.vue` 的 `projects` 陣列
- 純展示元件可以只有 `<template>`(如 `FooterBar.vue`),不必硬加空的 script
- 需要動畫時優先用 Tailwind utility;Tailwind 做不到的才在 `<style scoped>` 寫 `@keyframes`(如 Hero 的打字機游標)
- 有計時器或事件監聽時,務必在 `onUnmounted` 清理
- 不寫註解,除非是標示 template 區域的簡短英文註解(如 `<!-- background glow -->`)

## 驗收

改完後跑 `npm run build` 確認可建置。若環境可以開 preview,在瀏覽器確認新區塊與上下區塊的視覺銜接(背景色交替、間距一致)。
