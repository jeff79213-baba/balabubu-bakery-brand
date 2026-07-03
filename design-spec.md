# 設計規格書 · Purebread Bakery
> 把這份文件貼給任何 AI Agent，它就能用相同風格重建或擴展這個網站。

---

## 一、專案說明

**品牌名稱：** Purebread / 純粹麵包  
**類型：** 歐式手工烘焙坊官網  
**目標：** 質感、溫潤、高端，讓人感覺「這家店的麵包值得信賴」  
**參考風格：** 北歐極簡 × 法式溫度，不要科技感，不要陰影堆疊，不要圓角卡片

---

## 二、色盤（請嚴格使用以下 hex 值，不要自行調整）

| 名稱 | Hex | 用途 |
|------|-----|------|
| `--cream` | `#F7F3ED` | 頁面底色 |
| `--parchment` | `#EDE5D8` | 次要底色、分隔線 |
| `--warm-mid` | `#C9B99A` | 輔助色、標籤、線條 |
| `--espresso` | `#2C1F14` | 主要文字、深色背景 |
| `--ink` | `#3D2F22` | 內文 |
| `--dust` | `#8C7B68` | 次要文字、說明文 |
| `--white` | `#FDFAF6` | 卡片底色、反白文字 |

**禁止使用：** 純白 `#FFFFFF`、純黑 `#000000`、任何 Material Design 藍色系

---

## 三、字型

```
Google Fonts 載入：
- Cormorant Garamond (weights: 300, 400, 500 + italic)
- Noto Serif TC (weights: 300, 400)
- Inter (weights: 300, 400)
```

| 角色 | 字型 | 大小 | 字重 | 用途 |
|------|------|------|------|------|
| Display | Cormorant Garamond | 52–82px | 300 | 主標題、Hero |
| Heading | Cormorant Garamond | 24–40px | 400 | 商品名、章節標題 |
| Body ZH | Noto Serif TC | 14px | 300 | 中文內文、說明 |
| UI / Label | Inter | 9–11px | 300–400 | 導覽、標籤、按鈕文字 |

**字型規則：**
- 所有標籤、按鈕、導覽連結 → `letter-spacing: 0.18em` 以上，全大寫
- 主標題允許斜體 `<em>` 搭配正體混排，製造節奏感
- 絕對不要用 font-weight 700 以上

---

## 四、版型規則

```
最大寬度：無限制（全寬設計）
主要 padding：80px 左右（桌機）
網格：以 CSS Grid 為主，不用 Bootstrap 或任何 UI 框架
```

**禁止：**
- `border-radius` 超過 2px（幾乎不用圓角）
- `box-shadow`（不用任何陰影）
- `background: linear-gradient`（除了圖片覆蓋層的黑色漸層）
- Emoji 當圖示
- Font Awesome 或任何 icon library（如需圖示請用 inline SVG）

---

## 五、元件規格

### 導覽列 Nav
```css
height: 72px;
background: rgba(247,243,237,0.92);
backdrop-filter: blur(12px);
border-bottom: 1px solid rgba(201,185,154,0.25);
position: fixed;
```
- Logo：Cormorant Garamond 22px，letter-spacing 0.12em，全大寫
- 連結：Inter 11px，letter-spacing 0.18em，顏色 `--dust`，hover → `--espresso`

---

### 按鈕 Button
```css
/* Primary */
padding: 14px 40px;
border: 1px solid var(--espresso);
background: transparent;
font-size: 10px;
letter-spacing: 0.22em;
text-transform: uppercase;
color: var(--espresso);
/* hover */
background: var(--espresso);
color: var(--cream);
transition: 0.3s;
```
- 無圓角、無陰影、無漸層

---

### 商品卡片 Product Card
```
- 圖片區：正方形 (aspect-ratio: 1)，圖片 hover 時 scale(1.04) 6s ease
- 標籤：Inter 9px，letter-spacing 0.25em，顏色 --warm-mid
- 商品名：Cormorant Garamond 24px，weight 400，顏色 --espresso
- 說明：Inter/Noto 13px，顏色 --dust
- 底色：--white
- 卡片間距：2px gap（讓卡片緊貼，用縫隙而不是大間距分隔）
```

---

### 章節分隔線 Divider
```html
<div class="section-divider"><span>章節標題</span></div>
```
```css
display: flex; align-items: center; gap: 24px;
/* 左右兩條線用 ::before ::after，高度 1px，顏色 --parchment */
/* 文字：Inter 9px，letter-spacing 0.3em，顏色 --warm-mid */
```

---

### 橫幅 Band
```
- 高度：480px
- 覆蓋層：linear-gradient(to top, rgba(44,31,20,0.55) 0%, transparent 60%)
- 引言文字：Cormorant Garamond 斜體，28–48px，顏色 #FDFAF6
- 來源標籤：Inter 10px，letter-spacing 0.2em，顏色 rgba(253,250,246,0.55)
```

---

## 六、圖片規格（替換位置）

| 編號 | 位置 | 建議尺寸 | CSS 位置 |
|------|------|----------|----------|
| ① | Hero 主視覺 | 900 × 1080px | `.hero-image { background-image: url() }` |
| ② | 商品圖一 | 600 × 600px | `<img src="">` in `.product-card:nth-child(1)` |
| ③ | 商品圖二 | 600 × 600px | `<img src="">` in `.product-card:nth-child(2)` |
| ④ | 商品圖三 | 600 × 600px | `<img src="">` in `.product-card:nth-child(3)` |
| ⑤ | 橫幅大圖 | 1600 × 480px | `.band { background-image: url() }` |
| ⑥ | 關於我們 | 700 × 560px | `.about-image { background-image: url() }` |

**圖片風格建議：** 自然光、溫暖色調、不要過度飽和、不要加濾鏡

---

## 七、給 AI Agent 的指令範本

把以下這段連同本文件一起貼給 Agent：

```
請根據這份設計規格書，幫我完成以下任務：

[在這裡填入你的需求，例如：]
- 新增一個「門市資訊」頁面，風格與規格書完全一致
- 把這個網站部署到 Firebase Hosting
- 把 HTML 拆解成 React 元件，推送到 GitHub repo

規格書中的色碼、字型、間距規則請嚴格遵守，不要加入任何規格書以外的設計元素。
圖片統一用有標示的佔位區塊，我會自己替換。
```

---

## 八、技術規格

```
- 純 HTML + CSS（無框架依賴）
- Google Fonts CDN 載入
- CSS 變數管理所有色彩（:root 定義）
- RWD：桌機優先，手機版 padding 改為 24px，grid 改為 1 column
- 不使用 JavaScript 框架（互動效果用 CSS transition 完成）
- 若需要 JS：vanilla JS 即可，不引入 jQuery
```
