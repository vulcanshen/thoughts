# thoughts

Vulcan's design thoughts and notes.

跨專案的設計原則與觀察筆記。**一個目錄一個 topic**、每份文件只寫「該滿
足什麼」的 interface 層、不寫任何單一 app 的實作細節。

---

## Topics

### [tui-design](tui-design/) — VTP, My TUI Design Principle

回答的問題：**「在一個 terminal UI 上、什麼樣的設計能讓使用者不靠文件就
能用？」**

規定一套跨 surface、跨 app 不變的 core-key 語意與兩條動作揭露軌道，再
展開支撐它的分類規範（空間結構、色彩、互動、mouse、浮層、時間軸 UX;
符號語彙明確劃給各 app 自行決定）。跨 TUI app 通用、獨立於任何特定領域
或框架。
