# 綠天咖啡網站｜逆向詳細工程規格書 (Reverse Engineering Web Specification)

> **來源檔案**：`WebPage_11515107/outline/index.html`  
> **來源檔案雜湊 (SHA-256)**：`CA15AC60F160094F19D54A1C82F978E6171EA26DB08C7E8C040322E506F58405`  
> **來源程式碼規模**：2,634 行 / 84,770 位元組（單一自包含 HTML 文件）  
> **文件版本**：v2.0 (全站完整逆向工程規格版)  
> **文件用途**：依據現有完成之旗艦高階咖啡電商形象網頁，逆向拆解並建立完整規格文件，以利後續精確修改文字、調整商品參數、擴充購物車功能與重構組件。

---

## 1. 專案概述與商業定位

### 1.1 核心定義矩陣

| 項目 | 規格內容 | 備註說明 |
|---|---|---|
| **品牌全稱** | 綠天咖啡（GREEN SKY COFFEE） | 中英雙軌識別 |
| **網站性質** | 單頁式（SPA / Single-page）高階精品咖啡形象、選豆導購與沖煮文化推廣網站 | 兼具品牌展示與電商互動 |
| **主要客群 (Target Audience)** | 咖啡喜好者、手沖咖啡玩家、追求極限海拔與競標微批次風味的老饕、重度回購之品味鑑賞家 | 注重產地透明度與杯測評鑑 |
| **核心商業目標** | 1. 樹立高奢自然與職人慢焙品牌形象<br>2. 展示本季 4 款高階微批次選豆並驅動加入品味車<br>3. 透過首購折抵 $100 與滿額冷鏈免運促成即時轉化<br>4. 推廣每月 NT$ 1,280 產地月配訂閱俱樂部以建立長期回購<br>5. 收集微批次開賣電子報名單 | 雙軌導購：即時選購 + 定期訂閱 |
| **品牌核心語句 (Slogan)** | 「在極境雲嵐中，淬鍊高階咖啡的純粹。」 | Hero 主標題核心文案 |
| **網站形態** | 單一獨立 HTML 檔案，內嵌 CSS 與原生 JavaScript，無後端伺服器與建置工具相依 | 支援本機開箱即跑與靜態托管 |

### 1.2 品牌語氣與視覺哲學
- **視覺調性**：極致高奢、自然沉穩、莊園職人、簡約純粹、澄澈透光。
- **色彩策略**：以深邃墨林綠（`#0a1f16`）與翡翠深綠（`#1b4d36`）象徵高海拔原始雲霧林；佐以溫潤羊皮紙米白（`#f9f8f4`）維持閱讀舒適度；點綴典雅香檳金（`#c59f48`）強化高階競標與頂級精品尊榮感。
- **文案風格**：專業、克制、富有風土詩意，強調 SCA 國際杯測標準數據（海拔、烘焙度、處理法、品種、杯測分數）與感官風味描述。

---

## 2. 技術邊界與架構約束

1. **零外部建置工具**：不使用 Webpack, Vite, Tailwind CSS, Sass 或 TypeScript 編譯；所有程式碼整合於單一 `index.html`。
2. **語意化 HTML5**：結構遵循 `<aside.top-bar>`, `<header.site-header>`, `<main>`, `<section>`, `<article>`, `<footer>`，確保無障礙性與 SEO 爬蟲結構清晰。
3. **原生樣式 (Pure CSS3)**：
   - 採用 CSS 自訂變數（Custom Properties / CSS Tokens）管理全域色彩、陰影與圓角。
   - 排版核心採用 Flexbox 與 CSS Grid 混合系統。
   - 動態效果採用 CSS Keyframe 與硬體加速 transition。
4. **原生前端腳本 (Pure Vanilla JavaScript)**：
   - 不依賴 jQuery, Vue, React 或外部 UI 元件庫。
   - 採用 ES6+ 語法（箭頭函式、解構賦值、模板字串、`addEventListener`、`dataset` API、`navigator.clipboard` API）。
5. **字型資源外部相依**：
   - 僅透過 Google Fonts 引入 4 套專屬字體：`Noto Sans TC`（內文）、`Noto Serif TC`（中文襯線標題）、`Cinzel`（歐文典雅數據與徽章）、`Playfair Display`（歐文斜體展示）。
6. **零外部破圖風險**：
   - 全站無任何外部圖片 URL 相依。
   - 品牌 Crest 徽章、Hero 主視覺高階咖啡豆幾何圖形、評鑑星級、購物車圖示等皆採用內嵌 SVG 向量路徑或純 CSS 繪製。

---

## 3. SEO 與全域基礎設定

### 3.1 基礎 Meta 宣告
```html
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="綠天咖啡 GREEN SKY COFFEE — 專為咖啡喜好者嚴選高海拔微批次精品咖啡豆。以職人慢焙與產地純粹，呈現極致杯測風味。">
  <title>綠天咖啡 GREEN SKY COFFEE｜頂級高階咖啡豆・萃煉極致純粹</title>
  
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;600;700&family=Noto+Sans+TC:wght@300;400;500;600;700&family=Noto+Serif+TC:wght@400;600;700;900&family=Playfair+Display:ital,wght@0,600;0,700;1,600&display=swap" rel="stylesheet">
```

### 3.2 基礎樣式重置 (CSS Reset)
- `box-sizing: border-box` 套用於全域元素。
- `html` 啟用 `scroll-behavior: smooth` 與 `font-size: 16px`。
- `body` 背景色設定為 `var(--cream-bg)`，文字主色為 `var(--ink-primary)`，行高 `1.75`。
- 圖片預設 `max-width: 100%`, `display: block`。
- 按鈕預設移除原生邊框與背景，啟用 `cursor: pointer` 與 `transition`。

---

## 4. 設計系統規範 (Design Tokens)

### 4.1 品牌色彩系統 (Color Tokens)

```css
:root {
  --forest-dark: #0a1f16;    /* 墨林深綠：頁首、頁尾、深色區塊、主按鈕深色背景 */
  --forest-deep: #133324;    /* 森林深綠：卡片深色底、強調背景 */
  --emerald-dark: #1b4d36;   /* 翡翠深綠：主色按鈕、重點高亮 */
  --emerald-mid: #286348;    /* 翡翠中綠：邊框、副標強調、風味量條 */
  --sage-light: #82a893;     /* 鼠尾草綠：柔和強調、輔助標籤、頁尾次要文字 */
  --sage-pale: #e6f0ea;      /* 鼠尾草極淡綠：商品背景、徽章底、標籤底色 */
  --mint-glow: #a8e6cf;      /* 嫩芽明綠：夜間高光、頂部公告列文字 */
  --gold-accent: #c59f48;    /* 典雅香檳金：高階尊榮感、精品認證、星級評價 */
  --gold-light: #e5bd68;     /* 香檳金高光：字體高亮、徽章外圈光暈 */
  --cream-bg: #f9f8f4;       /* 溫潤羊皮紙米白：全站柔和底色 */
  --cream-surface: #ffffff;  /* 卡片主體純白 */
  --cream-subtle: #f3efe6;   /* 溫暖象牙米：交替區塊底色 (選豆區、評價區) */
  --ink-primary: #122119;    /* 深墨綠近黑：主文字閱讀 */
  --ink-muted: #53695d;      /* 沉靜霧綠：次要說明文字、規格欄位標籤 */
  --line-subtle: #dde8e1;    /* 淺綠柔和分隔線 */
  --line-gold: rgba(197, 159, 72, 0.35); /* 金色細邊框 */
  --shadow-sm: 0 4px 16px rgba(10, 31, 22, 0.06);
  --shadow-md: 0 14px 38px rgba(10, 31, 22, 0.1);
  --shadow-lg: 0 24px 60px rgba(10, 31, 22, 0.18);
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 16px;
  --transition-base: all 0.3s cubic-bezier(0.25, 1, 0.5, 1);
}
```

### 4.2 字體排印階層 (Typography Hierarchy)

| 類型 | 字型系列 (Font Family) | 典型規格 (大小 / 字重 / 行高 / 字距) | 套用元素 / 樣式類別 |
|---|---|---|---|
| **全站內文** | `"Noto Sans TC", sans-serif` | 15–16px / 400 / 1.75 / normal | `body`, `p`, `.step-desc`, `.pillar-text` |
| **英文典雅標籤** | `"Cinzel", serif` | 10–13px / 600–700 / 1.0 / 0.12em–0.26em | `.brand-text span`, `.eyebrow`, `.sca-score strong`, `.step-metric`, `.coupon-code` |
| **大展示主標題** | `"Noto Serif TC", serif` | `clamp(2rem, 3.8vw, 2.75rem)` / 700 / 1.35 / 0.04em | `.section-title`, `.hero-title` (`clamp(2.5rem, 5vw, 3.85rem)`) |
| **卡片標題** | `"Noto Serif TC", serif` | 1.25–1.5rem / 700 / 1.35 | `.bean-title`, `.pillar-title`, `.club-title` |
| **區塊眉標 (Eyebrow)** | `"Noto Sans TC", sans-serif` | 13px (0.8125rem) / 700 / 1.0 / 0.22em, 全大寫 | `.eyebrow` (左右帶 28px × 1px 裝飾線條) |
| **價格與數值** | `"Cinzel", "Noto Serif TC", serif` | 1.35–2.5rem / 700 | `.price-amount`, `.club-price` |

### 4.3 全域按鈕元件庫 (Button Components)

```css
/* 基礎按鈕規格 */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 14px 32px;
  font-size: 0.9375rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  border-radius: var(--radius-sm);
  transition: var(--transition-base);
}

/* 1. 香檳金漸層按鈕 (主要 CTA) */
.btn-gold {
  background: linear-gradient(135deg, #d4af37 0%, #b88a24 100%);
  color: #0d2117;
  font-weight: 700;
  box-shadow: 0 8px 24px rgba(184, 138, 36, 0.32);
}
.btn-gold:hover {
  background: linear-gradient(135deg, #e3be47 0%, #c99828 100%);
  transform: translateY(-2px);
  box-shadow: 0 12px 30px rgba(184, 138, 36, 0.45);
}

/* 2. 香檳金線框按鈕 (次要 CTA) */
.btn-outline-gold {
  border: 1px solid var(--gold-accent);
  color: var(--gold-accent);
  background: transparent;
}
.btn-outline-gold:hover {
  background: rgba(197, 159, 72, 0.12);
  color: #fff;
  border-color: #fff;
  transform: translateY(-2px);
}

/* 3. 翡翠綠按鈕 (商品購買、方案加入) */
.btn-emerald {
  background: var(--emerald-dark);
  color: #ffffff;
  box-shadow: 0 8px 20px rgba(27, 77, 54, 0.28);
}
.btn-emerald:hover {
  background: #235f43;
  transform: translateY(-2px);
  box-shadow: 0 12px 28px rgba(27, 77, 54, 0.38);
}

/* 4. 小型規格按鈕 */
.btn-sm {
  padding: 9px 20px;
  font-size: 0.8125rem;
}
```

---

## 5. 頁面資訊架構與 DOM 地圖 (Information Architecture)

全站採用由上至下單頁長流動式設計，包含 7 大主要語意區塊及 2 個全域互動覆蓋層：

```
body
├── aside.top-bar                     [頂部促銷公告列]
├── header.site-header#top            [頂部導覽列與品牌識別]
├── main
│   ├── section.hero-section          [1. Hero 旗艦主視覺區]
│   ├── section.philosophy-section#philosophy [2. 品牌哲學與四大標準]
│   ├── section.beans-section#selection       [3. 本季選豆核心展示區 + 促銷禮]
│   ├── section.club-section#club             [4. 產地風味月配訂閱俱樂部]
│   ├── section.brew-guide-section#guide      [5. 職人手沖萃取參數指南]
│   ├── section.review-section#reviews        [6. 顧客口碑與杯測師評價]
│   └── section.newsletter-section            [7. 電子報訂閱專區]
├── footer.site-footer                [網站頁尾資訊與品質承諾]
├── div.cart-drawer-overlay#cartOverlay [購物車側邊抽屜遮罩]
├── aside.cart-drawer#cartDrawer      [購物車側邊抽屜面板]
└── div.toast-msg#toastMsg            [全域 Toast 浮動反饋訊息]
```

### 全域錨點索引表

| 錨點 ID | 導覽名稱 | 目標區塊 | 功能說明 |
|---|---|---|---|
| `#top` | 返回頁首 | `header.site-header` | 點擊品牌 Logo 平滑滾動置頂 |
| `#selection` | 當季莊園豆 | `section.beans-section` | 直達選豆商品網格與風味篩選標籤 |
| `#philosophy` | 產地標準 | `section.philosophy-section` | 查看高海拔、人工摘選等 4 項標準 |
| `#club` | 尊享訂閱 | `section.club-section` | 了解每月 $1,280 莊園尋味方案 |
| `#guide` | 沖煮日常 | `section.brew-guide-section` | 查閱粉水比、水溫、悶蒸與注水參數 |
| `#reviews` | 杯測評鑑 | `section.review-section` | 查閱 Q-Grader 與主理人真實評價 |

---

## 6. 各區塊詳細規格與元件拆解

### 6.1 頂部促銷公告列 (`.top-bar`)
- **語意標籤**：`<aside class="top-bar">`
- **結構**：內包 `.wrap` 容器，置中排列。
- **文案內容**：
  > 極境尋味・全館滿 NT$1,200 即享黑貓冷鏈免運 ｜ 首購輸入折扣碼 **GREENSKY** 現抵 $100
- **視覺規範**：
  - 背景色：`#071710`（極深墨綠近黑）
  - 文字顏色：`var(--mint-glow)`（`#a8e6cf`），字級 `0.75rem`，字距 `0.14em`
  - 折扣碼高亮：`<strong>` 標籤，顏色 `var(--gold-light)`，附底線與指標游標（`cursor: pointer`）

### 6.2 網站全域導覽列 (`.site-header`)
- **語意標籤**：`<header class="site-header" id="top">`
- **佈局方式**：`position: sticky; top: 0; z-index: 1000;`
- **背景特效**：`background: rgba(10, 31, 22, 0.95); backdrop-filter: blur(12px);`
- **高度與邊框**：高 80px，底部邊框 `1px solid rgba(130, 168, 147, 0.2)`
- **主要組成子元件**：
  1. **品牌識別徽章與名稱 (`.brand-logo`)**：
     - `.brand-crest`：44px × 44px 圓形，金邊 1.5px，內嵌自定義 SVG 咖啡豆與幼葉路徑（顏色 `--gold-accent`）。
     - `.brand-text`：
       - `<h1>綠天咖啡</h1>`：`Noto Serif TC`, 1.35rem, 字重 700, 白色。
       - `<span>GREEN SKY COFFEE</span>`：`Cinzel`, 0.625rem, 字距 0.26em, 鼠尾草綠。
  2. **桌機導覽清單 (`.nav-menu`)**：
     - Flex 水平排列，間距 32px。
     - Hover 效果：文字漸變至 `--gold-light`，下方透過虛擬元素 `::after` 展開 1.5px 香檳金底線（動態寬度 0 → 100%）。
  3. **動作控制區 (`.nav-actions`)**：
     - **品味車按鈕 (`#openCartBtn.cart-trigger`)**：
       - 文字「品味車」+ 圓角計數徽章（`#cartCount.cart-badge`）。
       - 徽章背景色 `--gold-accent`，字色 `--forest-dark`，即時同步商品件數。
     - **行動版漢堡按鈕 (`#mobileToggleBtn.mobile-toggle`)**：
       - 圖示 `☰`，預設在寬度大於 768px 時 `display: none`。

---

### 6.3 Hero 旗艦主視覺區 (`.hero-section`)
- **語意標籤**：`<section class="hero-section" aria-labelledby="heroTitle">`
- **背景設定**：
  - 線性漸層背景：`linear-gradient(175deg, #091a12 0%, #102d20 50%, #0d2319 100%)`
  - 兩組氛圍虛擬元素：
    - `::before`：位於左上方，600px × 600px 墨綠徑向漸層，`filter: blur(80px)`
    - `::after`：位於右下方，500px × 500px 香檳金徑向漸層，`filter: blur(70px)`
- **排版結構**：網格雙欄（`grid-template-columns: 1.15fr 0.85fr; gap: 50px;`）

#### 左側內容欄位規格：
1. **動態微批次徽章 (`.hero-badge`)**：
   - 包含發光圓點 `.hero-badge-dot`（7px × 7px 金色圓形，套用 2 秒無限循環 `@keyframes pulseGlow` 動畫）。
   - 文字：`2026 春季高海拔珍稀微批次・產地直送`。
2. **主標題 (`#heroTitle.hero-title`)**：
   - 字體：`Noto Serif TC`, 字重 900, 大小 `clamp(2.5rem, 5vw, 3.85rem)`。
   - 文案：
     ```html
     在極境雲嵐中，<br>
     淬鍊<span class="gold-highlight">高階咖啡</span>的純粹。
     ```
   - 其中的 `.gold-highlight` 採用文字裁切漸層：`background: linear-gradient(135deg, #f7d57f 0%, #c59f48 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent;`。
3. **前言段落 (`.hero-desc`)**：
   - 文案：「綠天咖啡專注尋訪海拔 1,900 米以上的微型莊園。每一顆熟成紅果皆由雙手細緻摘選，透過直火低速慢焙，完整留存風土之中的細膩花香與澄澈回甘。」
4. **雙 CTA 按鈕組 (`.hero-cta-group`)**：
   - 主按鈕：`<a href="#selection" class="btn btn-gold">探索本季選豆 <span>→</span></a>`
   - 次按鈕：`<a href="#club" class="btn btn-outline-gold">尊享風味訂閱</a>`
5. **信任標章 (`.hero-trust`)**：
   - 項目 1：SVG 打勾圖示 + `SCA 國際杯測 88+ 卓越品質`
   - 項目 2：SVG 星星圖示 + `接單烘焙 72H 新鮮直送`

#### 右側高階品牌意象卡片 (`.hero-visual-card`)：
- 放射狀深林綠漸層背景，金邊 1px，頂部附 3px 金色線性漸層亮邊。
- **動態旋轉光環 (`.halo-ring`)**：220px 虛線圓圈，套用 `@keyframes rotateRing` 30 秒 360 度無縫線性旋轉。
- **極境咖啡豆 SVG (`.coffee-beans-svg`)**：
  - 140px × 140px 複合幾何，外環金線圓、內嵌翡翠綠旋轉橢圓及金色中心凹槽弧線。
- **獲獎標章 (`.card-award-tag`)**：`CUPPING MASTERPIECE`（Cinzel 字型，字距 0.22em）。
- **代表豆款名稱**：巴拿馬・翡翠莊園 藝妓（`HACIENDA LA ESMERALDA · SPECIAL RESERVE`）。
- **杯測分數藥丸標籤 (`.cupping-score-pill`)**：內嵌 `SCA 杯測評鑑 93.5 分`。

---

### 6.4 品牌哲學與四大嚴苛標準 (`.philosophy-section#philosophy`)
- **語意標籤**：`<section class="philosophy-section" id="philosophy">`
- **標題模組**：
  - Eyebrow：`OUR DISCIPLINE`
  - 主標：`為一杯極致，堅守四項嚴苛標準`
  - 副標：`高階咖啡的價值，來自於對自然風土的敬畏與每一個環節毫不妥協的專注。`
- **佈局網格**：4 欄卡片（`grid-template-columns: repeat(4, 1fr); gap: 24px;`）
- **四大標準內容明細**：

| 卡片編號 | 標準名稱 | 專業說明內容 |
|:---:|---|---|
| **01** | **1,900m+ 極境雲霧產區** | 只採購日夜溫差劇烈、雨量充沛的高海拔微型莊園。極限氣候賦予咖啡豆紮實密度與豐富的天然花果芳香物質。 |
| **02** | **100% 全人工逐粒紅果摘選** | 拒絕機械混採。莊園採收工僅採摘糖度達標的全熟紫紅咖啡果，在第一道關卡便剔除所有瑕疵，保證風味至純無雜。 |
| **03** | **微批次客製精密慢焙** | 採用德國頂級烘豆機，以秒為單位調校熱風比例與梅納反應節奏，完整展現每支產區豆專屬的酸甜平衡與產地特色。 |
| **04** | **純氮保鮮・杯測級防護** | 烘焙完成後經雙重光學色選，包裝注入 99.9% 食品級純氮氣並附單向排氣閥，完美封存開袋剎那的燦爛香氣。 |

- **懸停微動效**：懸停時 `transform: translateY(-6px)`，投影升級至 `--shadow-md`，外框亮起鼠尾草綠。

---

### 6.5 本季選豆核心展示區 (`.beans-section#selection`)
- **語意標籤**：`<section class="beans-section" id="selection">`
- **背景樣式**：溫暖象牙米色底（`var(--cream-subtle)`），上下均帶 1px 分隔線。
- **標題模組**：
  - Eyebrow：`HIGH-END SELECTION`
  - 主標：`品味本季高階莊園咖啡豆`
  - 副標：`嚴選全球知名產區微批次，每一款皆附產地追溯履歷與 SCA 國際杯測師品飲建議卡。`

#### 6.5.1 風味分類篩選器 (`.filter-tabs`)
- 包含 4 組 Tab 按鈕，具備 `data-filter` 屬性：
  1. `全部選豆 (4)` (`data-filter="all"`) —— 預設帶有 `.active` 類別
  2. `花果花香調` (`data-filter="floral"`)
  3. `特殊厭氧發酵` (`data-filter="wine"`)
  4. `醇厚堅果甘甜` (`data-filter="classic"`)

#### 6.5.2 咖啡豆商品資料模型矩陣 (4 大頂級豆款)

```
[商品 1: 巴拿馬 綠標藝妓] ── (category: floral, featured: true)
[商品 2: 衣索比亞 罕貝拉] ── (category: wine)
[商品 3: 肯亞 涅里高原]   ── (category: floral)
[商品 4: 哥倫比亞 酒桶蜜] ── (category: classic)
```

詳細商品技術數據對照表：

| 欄位項目 | 商品 1 (旗艦款) | 商品 2 | 商品 3 | 商品 4 |
|---|---|---|---|---|
| **商品全名** | 巴拿馬・翡翠莊園 綠標藝妓 | 衣索比亞・古吉 罕貝拉 G1 | 肯亞・涅里高原 AA TOP | 哥倫比亞・希望莊園 酒桶蜜處理 |
| **卡片標題** | 翡翠莊園 綠標藝妓 | 古吉 罕貝拉 G1 | 涅里高原 AA TOP | 希望莊園 酒桶蜜處理 |
| **產區 Meta** | PANAMA · BOQUETE | ETHIOPIA · GUJI HAMBELA | KENYA · NYERI HIGHLANDS | COLOMBIA · CAUCA |
| **分類別名** | `floral` | `wine` | `floral` | `classic` |
| **特殊標章** | 競標限定批次 (`.featured-ribbon`) | 無 | 無 | 無 |
| **SCA 杯測分數** | **93.5** | **91.2** | **90.8** | **92.0** |
| **生豆處理法** | 經典慢速水洗 | 72小時厭氧慢速日曬 | 肯亞傳統 72h 雙重水洗 | 橡木酒桶熟成黃蜜處理 |
| **種植海拔** | 1,850 - 2,050m | 2,100 - 2,300m | 1,950m | 1,800 - 2,000m |
| **烘焙度** | 淺焙 Light Roast | 淺中焙 Light-Medium | 淺焙 Light Roast | 中度烘焙 Medium |
| **咖啡品種** | 綠頂藝妓 Geisha | 衣索比亞原生種 Heirloom | SL28, SL34 | Castillo 特選 |
| **風味特徵標籤** | 白茉莉花、佛手柑、荔枝甜香、白桃餘韻 | 藍莓果醬、百香果、紅酒香脂、黑糖蜜感 | 黑醋栗、洛神花茶、紅葡萄柚、蔗糖清甜 | 威士忌麥香、太妃糖、烤榛果、可可絲滑 |
| **風味指標 1** | 花香感: 9.5 (95%) | 花果香: 9.0 (90%) | 果酸感: 9.4 (94%) | 香醇度: 9.6 (96%) |
| **風味指標 2** | 明亮酸: 8.8 (88%) | 酸甜質: 8.6 (86%) | 層次度: 9.0 (90%) | 醇厚感: 9.3 (93%) |
| **風味指標 3** | 甘甜度: 9.2 (92%) | 稠度感: 8.8 (88%) | 回甘感: 8.9 (89%) | 平衡性: 9.1 (91%) |
| **包裝規格** | 100g 充氮包裝 | 200g 充氮包裝 | 200g 充氮包裝 | 200g 充氮包裝 |
| **定價金額** | **NT$ 980** | **NT$ 580** | **NT$ 620** | **NT$ 720** |
| **購買按鈕樣式** | `.btn-gold.btn-sm` | `.btn-emerald.btn-sm` | `.btn-emerald.btn-sm` | `.btn-emerald.btn-sm` |
| **data-name** | `巴拿馬・翡翠莊園 綠標藝妓 (100g)` | `衣索比亞・古吉 罕貝拉 G1 (200g)` | `肯亞・涅里高原 AA TOP (200g)` | `哥倫比亞・希望莊園 酒桶蜜處理 (200g)` |
| **data-price** | `980` | `580` | `620` | `720` |

#### 6.5.3 促銷刺激橫幅 (`.promo-banner`)
- **定位**：放置於商品網格下方，直接激勵下單。
- **樣式**：深綠雙色漸層，金邊 1px，帶右上角柔和環境金光。
- **主標**：`初次相遇・全單折抵 $100 首購禮`
- **說明文案**：`喜愛頂級單品咖啡的您，結帳時輸入專屬迎賓優惠券即可現抵，滿額另享黑貓全程冷鏈溫控直送到府。`
- **優惠碼元件 (`.coupon-pill`)**：
  - 虛線金框藥丸背景，內含優惠碼 `#couponCodeText` (`GREENSKY`)。
  - 按鈕 `#copyCouponBtn`：點擊呼叫 Clipboard API 複製優惠碼並發出 Toast 提示。
- **一鍵轉化按鈕 (`#applyPromoToCartBtn`)**：
  - 點擊直接為購物車自動填入 `GREENSKY`、計算折扣並滑出購物車面板。

---

### 6.6 產地風味月配訂閱俱樂部 (`.club-section#club`)
- **語意標籤**：`<section class="club-section" id="club">`
- **佈局方式**：左右雙欄網格（`grid-template-columns: 1fr 1fr; gap: 50px;`）
- **左欄敘述**：
  - Eyebrow：`COFFEE SUBSCRIPTION`
  - 主標：`綠天尊享・產地風味訂閱俱樂部`
  - 段落 1：「每個月，我們為會員量身烘焙兩款當季微批次珍稀莊園豆。讓您不必費心挑選，在家就能同步品嚐全球頂尖競標級咖啡風土。」
  - 段落 2：「隨箱附贈莊園主產地故事卡、專業沖煮參數手冊，以及由 Q-Grader 精選的隱藏版試飲掛耳包。」
  - 按鈕組：
    - 加入訂閱：`<button class="btn btn-emerald" id="subscribeClubBtn">加入尊享訂閱方案</button>`
    - 沖煮指引連結：`<a href="#guide" class="btn btn-sm">了解沖煮指引</a>`
- **右欄月配卡片 (`.club-card-box`)**：
  - 高階黑綠金邊漸層卡片，帶有柔和金光陰影。
  - 徽章：`MONTHLY EXCLUSIVE CLUB`
  - 標題：`莊園尋味月配方案`
  - 價格：`NT$ 1,280 / 每月（免運直送）`
  - 4 大會員權益清單（金色打勾圖示）：
    1. 每月精選 2 款高階莊園單品豆（共 400g，約可沖煮 26 杯）
    2. 享優先認購年度 COE（卓越杯）微批次特權
    3. 每月隨贈原木咖啡匙或精品濾紙等精選週邊
    4. 隨時可彈性暫停或取消，無綁約壓力
  - 快速加入按鈕：`<button class="btn btn-gold" id="directJoinClubBtn">立即開啟每月風味驚喜</button>`
  - **JS 互動邏輯**：點擊 `#subscribeClubBtn` 或 `#directJoinClubBtn` 都會將「綠天尊享・微批次月配方案 (2袋共400g)」以 NT$ 1,280 加入品味車，並立即滑出購物車抽屜。

---

### 6.7 職人手沖萃取參數指南 (`.brew-guide-section#guide`)
- **語意標籤**：`<section class="brew-guide-section" id="guide">`
- **標題模組**：
  - Eyebrow：`BREWING COMPASS`
  - 主標：`高階豆的最佳手沖萃取參數`
  - 副標：`好的豆子需要合宜的水溫與時間相伴。遵循綠天黃金萃取指引，輕鬆在家還原杯測室的澄澈風味。`
- **佈局網格**：4 欄步驟卡片（`grid-template-columns: repeat(4, 1fr); gap: 24px;`）
- **步驟參數細節**：

| 步驟序號 | 關鍵參數指標 | 核心標題 | 萃取指南詳細說明 |
|:---:|---|---|---|
| **1** | **15g : 240ml** | 黃金粉水比 1:16 | 建議研磨刻度為中細度（約如二砂糖顆粒），既能充分帶出花果酸質，又維持尾韻清爽無苦澀。 |
| **2** | **91°C - 93°C** | 理想萃取水溫 | 淺焙豆適合 92°C 展現明亮酸甜；中焙與酒桶蜜處理建議降至 90°C，以突顯絲滑可可與焦糖酒香。 |
| **3** | **35 秒** | 充分悶蒸呼吸 | 以 35ml 熱水自中心穩定繞圈浸潤咖啡粉層，靜候排氣隆起，喚醒休眠的天然芳香分子。 |
| **4** | **2'30"** | 平穩分段注水 | 分兩段均勻慢速注水至 240ml，保持水流細緻平穩，於 2 分 30 秒至 2 分 45 秒萃取完畢。 |

---

### 6.8 顧客口碑與杯測師評價 (`.review-section#reviews`)
- **語意標籤**：`<section class="review-section" id="reviews">`
- **標題模組**：
  - Eyebrow：`CONNOISSEUR TESTIMONIALS`
  - 主標：`來自咖啡愛好者與專業杯測師的評價`
  - 副標：`唯有真實細緻的風味體驗，才能贏得老饕與行家反覆回購的信賴。`
- **佈局網格**：3 欄評價卡片（`grid-template-columns: repeat(3, 1fr); gap: 28px;`）
- **評價卡片細節明細**：

```
[卡片 1: SCA 國際高級杯測師 林柏翰] ── 評價翡翠莊園藝妓水洗乾淨度
[卡片 2: 資深手沖愛好者 張雅涵]   ── 評價充氮保鮮與俱樂部開箱體驗
[卡片 3: 精品咖啡館主理人 陳品睿] ── 評價古吉罕貝拉莓果甜感與黑糖蜜餘韻
```

| 評鑑者姓名 | 身份與資歷認證 | 頭像字 | 星級評分 | 口碑引言內容 |
|---|---|:---:|:---:|---|
| **林柏翰 先生** | SCA 國際認證高級杯測師 (Q-Grader) | 林 | ★★★★★ | 「翡翠莊園藝妓的水洗表現令人驚艷，白茉莉與柑橘香氣如同在杯中盛開，乾淨度極高，完全對得起高階莊園豆的價位！」 |
| **張雅涵 小姐** | 資深手沖愛好者・台北 | 張 | ★★★★★ | 「已經訂閱綠天俱樂部半年，每個月收到開箱都像收到珍貴禮物。充氮保鮮做得很扎實，開袋那一刻香氣撲鼻，天天都期待手沖時刻。」 |
| **陳品睿 先生** | 精品咖啡館主理人 | 陳 | ★★★★★ | 「古吉罕貝拉的果醬與莓果甜感非常濃郁，按照官方提供的 92 度水溫沖煮，尾韻的黑糖蜜甜感持久不散，絕對會再回購！」 |

---

### 6.9 電子報訂閱專區 (`.newsletter-section`)
- **語意標籤**：`<section class="newsletter-section">`
- **樣式**：深邃雙色墨綠漸層，居中排版，金線頂部分隔。
- **Eyebrow**：`EXCLUSIVE ACCESS`
- **主標**：`獲取珍稀微批次開賣第一手通知`
- **副標說明**：`訂閱綠天咖啡風味通訊，每週分享產地採購紀實、最新批次杯測評分，並獲取會員專屬特惠碼。`
- **表單互動元件 (`#newsletterForm.newsletter-form`)**：
  - 電子信箱輸入框：`<input type="email" placeholder="輸入您的電子信箱" required aria-label="電子郵件">`
  - 送出按鈕：`<button type="submit">訂閱獲取折扣券</button>`（金色底深色字）
  - **JS 互動**：監聽 `submit` 事件，`preventDefault()` 阻止頁面跳轉，重設表單並跳出 Toast：「感謝訂閱！首購優惠碼 GREENSKY 已發送至您的信箱。」

---

### 6.10 網站頁尾資訊 (`.site-footer`)
- **語意標籤**：`<footer class="site-footer">`
- **背景與排版**：極深墨黑底色（`#06130d`），內部 4 欄網格（`grid-template-columns: 1.5fr 1fr 1fr 1.2fr; gap: 40px;`）
- **欄位規劃**：
  1. **品牌宗旨 (Col 1)**：
     - 縮小版 Brand Logo（36px 圓徽章 + 雙行標題）。
     - 核心引言：「讓風味在晨光微風中甦醒。為注重生活細節的你，尋訪世界極境莊園，敬呈一杯值得靜心的極致好咖啡。」
  2. **探索咖啡 (Col 2)**：
     - 快速錨點連結：當季單品豆 (`#selection`)、產地品質標準 (`#philosophy`)、尊享訂閱計劃 (`#club`)、沖煮參數指引 (`#guide`)。
  3. **品飲門市與體驗 (Col 3)**：
     - 門市地址：台北市大安區青田街 28 號
     - 營業時間：每日營業：10:00 — 18:30
     - 預約電話：(02) 2391-7890
     - 客服信箱：concierge@greensky.coffee
  4. **品質承諾 (Col 4)**：
     - 說明：「本站所有咖啡豆皆投保一千萬元產品責任險，全系列包裝採用日本進口單向排氣充氮鋁箔袋。」
     - 認證勾選標記：
       - `✓ SCA 國際咖啡品質標準評定`
       - `✓ 100% 莊園單一品種產地透明`
- **底部版權宣告 (`.footer-bottom`)**：
  - 左側：`© 2026 綠天咖啡 GREEN SKY COFFEE. ALL RIGHTS RESERVED.`
  - 右側：`HIGHLAND TERROIR · ARTISAN ROASTED · PURE CRAFT`

---

### 6.11 品味車側邊抽屜互動模組 (`.cart-drawer`)
- **語意結構**：
  - 背景遮罩：`<div class="cart-drawer-overlay" id="cartOverlay"></div>`
  - 側邊抽屜本體：`<aside class="cart-drawer" id="cartDrawer" aria-label="購物車內容">`
- **尺寸與定位**：`position: fixed; top: 0; right: 0; width: min(440px, 100%); height: 100vh; z-index: 2001;`
- **滑入動效**：預設 `transform: translateX(100%)`，加上 `.active` 時平滑滑入 `transform: translateX(0)`，配合 `body` 鎖定滾動（`overflow: hidden`）。
- **結構組成**：
  1. **抽屜頁首 (`.cart-header`)**：
     - 標題：「您的品味清單 (<span id="cartTotalItems">0</span>)」
     - 關閉按鈕：`<button class="close-cart-btn" id="closeCartBtn">✕</button>`
  2. **商品清單容器 (`#cartItemsContainer.cart-items-list`)**：
     - **空車狀態 (`#cartEmptyState`)**：顯示購物車空狀態 SVG 圖示 +「品味車尚無選豆，立即挑選喜愛的莊園風味吧！」。
     - **商品列 (`.cart-item-row`)**：動態生成，包含品名、單價與 `+` / `-` 數量控制鈕組。
  3. **抽屜頁尾計價區 (`.cart-footer`)**：
     - **折扣碼輸入群組 (`.cart-coupon-input`)**：輸入框 `#couponInput` + 套用按鈕 `#applyCouponBtn`。
     - **折扣顯示列 (`#discountRow`)**：顯示「首購優惠折扣」與 `- NT$ 100`（未折抵時 `display: none`）。
     - **小計金額列 (`.cart-subtotal`)**：顯示「小計金額」與 `#cartTotalPrice`。
     - **結帳按鈕 (`#checkoutBtn`)**：金色主按鈕「立即結帳享風味直送」。

---

### 6.12 全域 Toast 浮動通知 (`.toast-msg`)
- **語意標籤**：`<div class="toast-msg" id="toastMsg" role="status" aria-live="polite">已加入購物車</div>`
- **位置與外觀**：固定於右下角（`bottom: 24px; right: 24px; z-index: 3000;`），深墨綠底，左側帶 4px 香檳金亮邊條。
- **過渡動效**：預設透明且下移 20px（`opacity: 0; transform: translateY(20px)`），套用 `.show` 類別時滑升浮現，延遲 2.8 秒自動消退。

---

## 7. JavaScript 狀態架構與互動邏輯

### 7.1 前端資料狀態模型 (Data State Model)

```javascript
// 購物車項目結構
let cart = [
  // 結構型別：
  // {
  //   name: string,      // 商品完整品名規格，例如 "巴拿馬・翡翠莊園 綠標藝妓 (100g)"
  //   price: number,     // 單價數值 (NT$)，例如 980
  //   quantity: number   // 購買件數，預設 1
  // }
];

let discountAmount = 0;   // 目前折抵金額 (預設 0，符合優惠碼條件折抵 100)
let appliedCoupon = '';    // 目前套用之代碼字串 (例如 'GREENSKY')
```

### 7.2 核心函式邏輯詳細規格

```
[用戶點擊「加入品味車」] ──> addToCart(name, price) ──> 更新 cart 陣列 ──> renderCart() ──> showToast()
[用戶點擊「品味車」按鈕] ──> toggleCart(true) ──> 抽屜加入 .active ──> body 鎖定滾動
[用戶修改數量 (+/-)]    ──> 委派事件監聽 ──> 變更 quantity ──> 若 quantity<=0 則剔除 ──> renderCart()
[用戶輸入折扣碼]        ──> applyCoupon() ──> 檢查 'GREENSKY' 與購物車長度 ──> discountAmount=100 ──> renderCart()
[用戶點擊「結帳」]      ──> 檢驗 cart 長度 ──> alert() 建立訂單 ──> 清空狀態 ──> renderCart() ──> toggleCart(false)
```

#### 1. `showToast(text)`
- 清除前次 `toastTimeout`。
- 更新 `#toastMsg` 文字內容。
- 新增 `.show` 類別。
- 透過 `setTimeout` 設定 2,800ms 後移除 `.show`。

#### 2. `toggleCart(open)`
- 若 `open === true`：`cartDrawer` 與 `cartOverlay` 新增 `.active`，`document.body.style.overflow = 'hidden'`。
- 若 `open === false`：移除 `.active`，恢復 `document.body.style.overflow = ''`。
- 監聽 `#openCartBtn` (開啟)、`#closeCartBtn` (關閉)、`#cartOverlay` (點擊背景關閉)。

#### 3. `renderCart()`
- 計算購物車總件數：`totalCount = cart.reduce((sum, item) => sum + item.quantity, 0)`。
- 即時更新導覽列計數徽章 `#cartCount` 與抽屜內標題 `#cartTotalItems`。
- 若 `cart.length === 0`：
  - 顯示 `#cartEmptyState`。
  - 清空所有 `.cart-item-row`。
  - `#cartTotalPrice` 歸零 (`NT$ 0`)。
  - 隱藏 `#discountRow` 並重置 `discountAmount = 0`。
- 若 `cart.length > 0`：
  - 隱藏 `#cartEmptyState`。
  - 計算原始總額：`rawTotal = sum(item.price * item.quantity)`。
  - 依據 `cart` 動態渲染每筆項目行，插入 `.qty-btn`（帶 `data-action` 與 `data-index`）。
  - 計算最終總額：`finalTotal = Math.max(0, rawTotal - discountAmount)`。
  - 顯示千分位格式總價：`NT$ ${finalTotal.toLocaleString()}`。
  - 若 `discountAmount > 0` 則顯現折扣列，標示 `- NT$ 100`。

#### 4. `addToCart(name, price)`
- 呼叫 `cart.find(item => item.name === name)` 檢查是否已有相同品名。
- 若已有該商品，其 `quantity += 1`；若無，則 `push({ name, price: Number(price), quantity: 1 })`。
- 執行 `renderCart()`。
- 呼叫 `showToast('已將「' + name + '」加入品味車')`。

#### 5. 購物車數量增減委派監聽 (`cartItemsContainer.addEventListener('click')`)
- 透過 `e.target.closest('.qty-btn')` 取得點擊目標。
- 讀取 `btn.dataset.action` 與 `btn.dataset.index`。
- 若 `action === 'increase'`：`cart[index].quantity += 1`。
- 若 `action === 'decrease'`：`cart[index].quantity -= 1`，若數量歸零則透過 `cart.splice(index, 1)` 自陣列刪除。
- 重新呼叫 `renderCart()`。

#### 6. 折扣碼驗證邏輯 (`applyCoupon()`)
- 取得 `#couponInput.value.trim().toUpperCase()`。
- 驗證條件分歧：
  - 若代碼等於 `'GREENSKY'`：
    - 若 `cart.length === 0`：提示「請先加入喜愛的咖啡豆再套用折扣碼」。
    - 若 `cart.length > 0`：設定 `discountAmount = 100`，`appliedCoupon = 'GREENSKY'`，呼叫 `renderCart()`，提示「成功折抵 NT$ 100 首購優惠券！」。
  - 若代碼為空：提示「請輸入折扣碼」。
  - 其他代碼：提示「折扣碼無效，請確認後再試」。

#### 7. 快速領取優惠按鈕 (`#applyPromoToCartBtn`)
- 點擊後自動將輸入框填入 `'GREENSKY'`。
- 自動呼叫 `applyCoupon()`。
- 自動呼叫 `toggleCart(true)` 滑出購物車。

#### 8. 剪貼簿複製折扣碼 (`#copyCouponBtn`)
- 呼叫 `navigator.clipboard.writeText('GREENSKY')`。
- 成功時 Toast 回饋：「已複製優惠碼 GREENSKY，可在結帳時貼上套用！」。
- 失敗降級 Toast：「優惠代碼為 GREENSKY」。

#### 9. 訂閱俱樂部加入品味車 (`#subscribeClubBtn`, `#directJoinClubBtn`)
- 呼叫 `addToCart('綠天尊享・微批次月配方案 (2袋共400g)', 1280)`。
- 自動呼叫 `toggleCart(true)` 開啟品味車。

#### 10. 結帳模擬邏輯 (`#checkoutBtn`)
- 若 `cart.length === 0`：Toast 提示「品味車內尚未有選豆，請先挑選商品」。
- 若 `cart.length > 0`：
  - 彈出原生對話框：`感謝您選購綠天咖啡！\n系統已為您建立訂單，我們將於 24 小時內新鮮現烘，並以冷鏈配送寄出。`
  - 重設 `cart = []`, `discountAmount = 0`, `appliedCoupon = ''`, `couponInput.value = ''`。
  - 呼叫 `renderCart()` 與 `toggleCart(false)`。

#### 11. 風味標籤分類篩選 (`.tab-btn`)
- 點擊各 Tab 時，先清除所有 Tab 的 `.active`，並為當前點擊項添加 `.active`。
- 取得點擊之 `data-filter`。
- 遍歷所有 `.bean-card`：
  - 若 `filter === 'all'` 或 `card.dataset.category === filter`：`card.style.display = 'flex'`。
  - 否則：`card.style.display = 'none'`。

#### 12. 電子報表單處理 (`#newsletterForm`)
- 監聽 `submit` 事件並阻止預設行為。
- 發送 Toast：「感謝訂閱！首購優惠碼 GREENSKY 已發送至您的信箱。」。
- 呼叫 `newsletterForm.reset()` 清空輸入內容。

#### 13. 行動版選單切換 (`#mobileToggleBtn`)
- 點擊 `#mobileToggleBtn` 時，為 `#navMenu` 切換 `.open` 類別。
- 點擊 `#navMenu a` 任一錨點連結後，自動移除 `.open` 關閉選單。

---

## 8. 響應式佈局規格 (Responsive Design / RWD)

全站採用 Fluid + 雙主要斷點設計：

```
[桌面寬螢幕 > 992px]  ──> Hero 雙欄, 四大標準 4 欄, 選豆 3 欄, 沖煮指南 4 欄, 評價 3 欄, 頁尾 4 欄
[平板模式 <= 992px]   ──> Hero 單欄居中, 四大標準 2 欄, 選豆 2 欄, 沖煮指南 2 欄, 評價 1 欄, 頁尾 2 欄
[手機直向 <= 768px]   ──> 導覽轉漢堡下抽選單, 選豆 1 欄, 四大標準 1 欄, 促銷橫幅單欄, 頁尾 1 欄
```

### 8.1 平板與中型螢幕斷點 (`@media (max-width: 992px)`)
1. **Hero 旗艦主視覺**：
   - 網格改為單欄 `grid-template-columns: 1fr; text-align: center;`。
   - 前言段落、雙 CTA 按鈕與信任標章皆改為水平居中對齊。
2. **四大標準網格 (`.pillars-grid`)**：由 4 欄改為 2 欄（`repeat(2, 1fr)`）。
3. **選豆商品網格 (`.beans-grid`)**：由 3 欄改為 2 欄（`repeat(2, 1fr)`）。
4. **訂閱俱樂部網格 (`.club-grid`)**：改為單欄（`1fr`），卡片上下疊放。
5. **手沖參數指南 (`.guide-steps-grid`)**：由 4 欄改為 2 欄（`repeat(2, 1fr)`）。
6. **口碑評價網格 (`.reviews-grid`)**：改為單欄滿版（`1fr`）。
7. **頁尾網格 (`.footer-grid`)**：改為雙欄佈局（`1fr 1fr`）。

### 8.2 手機直向斷點 (`@media (max-width: 768px)`)
1. **導覽列改為漢堡抽屜選單**：
   - 行動開關 `#mobileToggleBtn` 轉為 `display: block`。
   - 導覽選單 `#navMenu` 改為 `position: fixed; top: 80px; left: 0; right: 0;`。
   - 垂直排列，背景為墨林深綠（`var(--forest-dark)`），帶底部金邊。
   - 預設收合至螢幕上方（`transform: translateY(-150%)`），加上 `.open` 類別時展開（`transform: translateY(0)`）。
2. **商品與規格網格**：
   - 選豆網格 `.beans-grid` 改為單欄（`1fr`）。
   - 四大標準 `.pillars-grid` 改為單欄（`1fr`）。
   - 沖煮指南 `.guide-steps-grid` 改為單欄（`1fr`）。
3. **促銷橫幅 (`.promo-flex`)**：改為垂直置中排列（`flex-direction: column; text-align: center;`）。
4. **頁尾網格 (`.footer-grid`)**：改為單欄縱向排列（`1fr`）。
5. **頁尾版權列 (`.footer-bottom`)**：由左右對齊改為垂直堆疊置中（`flex-direction: column; gap: 10px;`）。
6. **購物車抽屜**：寬度由固定 440px 自動縮放至螢幕寬度滿版（`width: min(440px, 100%)`）。

---

## 9. 無障礙與使用者體驗規範 (A11y & UX)

1. **語意結構健全**：正確應用 `<aside>` 標註頂部公告列與購物車抽屜；使用 `<main>` 包含主要內容區塊。
2. **ARIA 宣告完善**：
   - 購物車側邊抽屜配置 `aria-label="購物車內容"`。
   - Toast 浮動反饋配置 `role="status"` 與 `aria-live="polite"`，確保螢幕報讀軟體能即時朗讀狀態更新。
   - 表單輸入框配置明確之 `aria-label`。
   - 圖示 SVG 均配置 `aria-hidden="true"`，避免重複發音干擾。
3. **視覺對比度 (Contrast Ratio)**：
   - 墨林深綠背景（`#0a1f16`）對比白色文字（`#ffffff`）超過 14:1。
   - 香檳金亮色（`#e5bd68`）對比深綠底色超過 8:1。
   - 滿足 WCAG 2.1 AAA 級最高可讀性規範。
4. **操作回饋**：
   - 加入品味車、套用折扣、複製優惠代碼、訂閱電子報皆有即時 Toast 反饋。
   - 抽屜開啟時鎖定背景捲動，防止雙重滾動穿透。

---

## 10. 後續修改、精確維護與擴展實作指南

### 10.1 如何新增或替換當季咖啡豆品項
若需新增或修改選豆，直接在 `outline/index.html` 的 `#selection .beans-grid` 內編輯 `<article class="bean-card">`：
1. **設定篩選分類**：在 `<article>` 上設定 `data-category="floral|wine|classic"`。
2. **設定產地與標題**：修改 `.bean-meta-top` 與 `.bean-title`。
3. **設定 SCA 分數**：更新 `.sca-score strong` 內的數值。
4. **設定四項參數清單**：維護處理法、種植海拔、烘焙度與品種。
5. **設定三維風味條**：調整 `.meter-row` 的數值（例如 `9.2`）以及對應 `.meter-fill` 的寬度百分比（例如 `style="width: 92%;"`）。
6. **設定規格價格與購物車屬性**：
   - 修改 `.price-amount` 顯示文字（例如 `NT$ 650`）。
   - **關鍵同步**：務必確保 `.add-to-cart-btn` 上的 `data-name` 與 `data-price` 數值正確，以利 JavaScript 讀取。

### 10.2 如何新增風味標籤分類 (Filter Tab)
1. 於 `.filter-tabs` 增加 `<button class="tab-btn" data-filter="新分類名">新分類中文</button>`。
2. 將欲歸類至該標籤的咖啡豆卡片標籤加上 `data-category="新分類名"` 即可自動支援無縫切換。

### 10.3 如何調整折扣優惠碼與額度
於 `<script>` 區塊內的 `applyCoupon()` 函式進行調整：
```javascript
// 修改優惠代碼判定與折抵金額
if (code === 'GREENSKY_VIP') {
  discountAmount = 150; // 調整為折抵 150
  appliedCoupon = 'GREENSKY_VIP';
}
```

### 10.4 如何平滑升級串接後端電商 API
目前結帳點擊事件採用前端模擬：
```javascript
checkoutBtn.addEventListener('click', () => { ... });
```
可將模擬邏輯無痛抽換為真實 API 呼叫：
```javascript
fetch('/api/v1/orders', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    items: cart,
    coupon: appliedCoupon,
    discount: discountAmount
  })
})
.then(res => res.json())
.then(order => {
  window.location.href = `/checkout/payment?orderId=${order.id}`;
});
```

---

## 11. 驗收核對清單 (Acceptance Criteria)

- [x] **品牌識別完整**：網站名稱為「綠天咖啡 GREEN SKY COFFEE」，標題與 Logo 向量無誤。
- [x] **色彩系統精確**：全面導入墨林深綠、翡翠綠、鼠尾草綠、羊皮紙米白與香檳金。
- [x] **4 款高階豆完整呈現**：產地、處理法、海拔、烘焙度、SCA 分數、風味雷達與售價精確對應。
- [x] **風味分類篩選功能**：4 個 Tab 正確切換卡片顯隱。
- [x] **品味車抽屜功能**：支援商品新增、數量增加、數量減少（減至 0 自動刪除）、即時動態小計。
- [x] **優惠代碼折抵機制**：輸入 `GREENSKY` 成功現折 NT$ 100，支援點擊複製與促銷橫幅一鍵帶入。
- [x] **產地月配俱樂部**：NT$ 1,280 方案點擊後自動加入品味車並滑出抽屜。
- [x] **手沖指南四步驟**：粉水比、水溫、悶蒸、注水完整呈現。
- [x] **真實口碑評價與電子報**：3 組評價內容與電子報表單防刷新 Toast 提示。
- [x] **響應式佈局 (RWD)**：992px 平板雙欄與 768px 手機漢堡選單開合正常無破版。
- [x] **單一檔案無外部破圖**：所有圖示與幾何插圖純原生 SVG/CSS 實作。
