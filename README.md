# thoughts

Vulcan's design thoughts and notes.

跨專案的設計原則與觀察筆記。這裡只放**「該滿足什麼」**的 interface 層文
件、不放任何單一 app 的實作細節。

---

## [VTP — Vulcan's TUI Design Principle](vtp.md)

一份跨 TUI app 的通用設計原則、獨立於任何特定領域或框架（K8s / Bubble
Tea / Lipgloss 等）。

回答的問題：**「在一個 terminal UI 上、什麼樣的設計能讓使用者不靠文件就
能用？」**

### VTP score

VTP 不是「有 / 沒有」的 binary、是 0%–100% 的連續分數、由兩個設計可控軸
合成：

```
VTP score = X × min(1, 5/Y) × 100%
```

| 軸 | 定義 | 說明 |
|---|---|---|
| **X — 揭露程度** | core-key 入口可直接看到並執行的操作數 ÷ app 全部操作數 | 任何「藏起來」的操作都把 X 拉低 |
| **Y — core-key role 數量** | 兩條 track 用到的 role 聯集大小（alias 共用 role 算 1 個）| Y ≤ 5 無 penalty、超過線性扣分 |

對照例：

| App | VTP score |
|---|:---:|
| kbu（entry-key + interactive menu）| ~100% |
| nano（ambient cheatsheet + `^G`）| ~100% |
| vim 默認（prompt-style、不揭露）| 0% |
| vim + which-key / LazyVim | 接近 100% |

vim core 一字未動、LazyVim 疊加一個揭露 layer 就從 0 跳到接近 100 —
**VTP 跟 app core 可分離、是可疊加的 layer**。

VTP 高 ≠ 好 app、低 ≠ 爛 app。它只度量「不需事先學習就能用」這一個
dimension、跟 hotkey ergonomics、學會後效率、composability 等維度獨立。

### 文件結構

| 章節 | 內容 |
|---|---|
| §0 Meta | Guide serves UX, not the other way — 規則跟 UX 衝突時 UX 贏 |
| 術語定義 | Surface / Focus / Contextual 與 Non-contextual 動作 |
| §A. VTP 核心 | 目標層：基礎操作貫穿全 app、VTP score 定義、core-key ≤ 5 |
| §B. 元素專職化 | 機制層：一個元素、一個語意、不兼職 |
| 1. 空間結構 | 窄寬可用測試、width stability、footer 行數固定 |
| 2. 色彩 | 最少必要錨點、明度作 z-axis、顏色帶專職化 |
| 3. 符號語彙 | 圖示字體是設計不是 optional、glyph 可靠子集 |
| 4. 互動 | Core key set 跨全 app 一致、hotkey 完整性與 discoverability |
| 5. Mouse | 唯一的負面規範：mouse 必為 keyboard 的 mapping、不引入新語意 |
| 6. 浮層 | 浮層分類、動畫、border 色、stack 行為、錯誤呈現 |
| 7. 時間軸 UX | 只在 user flow 上才存在、靜止截圖看不出來的原則 |

> 本文件是 **interface**。某個 app 怎麼具體 implement、寫在它自己的
> implementation doc 裡（`kbu-implementation.md`、`filu-implementation.md`）。
