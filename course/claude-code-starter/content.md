# 認識 Claude Code：你的超級超級厲害 AI 開發夥伴
> Claude Code 不是聊天機器人，而是能直接讀寫你的程式碼、執行指令、操作檔案的 AI 開發助手

## 什麼是 Claude Code？

### 🤖 從聊天到真正行動
- 一般 AI 工具：你提問 → AI 回答文字 → 你手動複製貼上
- Claude Code：你提問 → AI 直接修改檔案、執行指令、完成任務
- 差異：**AI 有了真實的行動能力**，不只是建議，而是直接做

### 🛠️ Claude Code 能做什麼？
- 讀取與修改專案中的任意程式碼
- 執行 shell 指令（npm install、git commit、測試等）
- 搜尋程式碼庫、理解專案架構
- 瀏覽器截圖、讀取 PDF / 圖片
- 透過 MCP 連接外部服務（GitHub、資料庫、Slack 等）

> **不是「AI 幫你寫程式」，而是「AI 跟你一起開發」**
> 傳統 Copilot 是補全工具，Claude Code 更像一個能獨立工作的開發夥伴。你負責把關方向，AI 負責執行細節。

### 📊 適合誰用？

[tags]
- [green] 工程師：加速重複性工作、快速理解陌生程式碼
- [blue] 技術主管：Code Review、架構規劃、文件生成
- [purple] 非工程師：用自然語言驅動程式碼，降低技術門檻
- [orange] 初學者：邊做邊學，AI 即時解說每一行在做什麼
[/tags]

## 安裝與環境設定

### ⚙️ 安裝 Claude Code

[flow]
1. 確認 Node.js 環境（建議 v18+）
2. 使用 npm 安裝 Claude Code CLI
3. 登入 Anthropic 帳號完成授權
4. 在專案目錄執行 `claude` 啟動
[/flow]

```prompt [label="安裝指令"]
npm install -g @anthropic-ai/claude-code
```

```prompt [label="啟動 Claude Code"]
claude
```

### 🔑 費用與方案說明
- **Pro 方案**：每月固定費用，包含 Claude Code 使用額度
- **API 方案**：按用量計費，適合進階使用者
- 建議新手從 Pro 方案開始，上手後評估是否切換

> **一開始不要擔心費用**
> 學習階段的用量通常不高。真正大量使用 Claude Code 時，你的效率早已抵銷成本了。

---

# 核心操作：掌握日常開發節奏
> 工具好不好用，差別在細節；掌握這些操作模式，你的開發速度會有質變

## 對話模式與指令

### 💬 對話的藝術：怎麼問才有效？

[flow]
1. 描述「目標」，而非「步驟」
2. 提供足夠的上下文（檔案位置、技術棧）
3. 遇到問題時，補充「預期行為 vs 實際行為」
[/flow]

```prompt [label="有效的提問範例"]
這個 login API 回傳 401，但帳密是正確的。
請查看 src/api/auth.ts 和 middleware/jwt.ts，找出問題原因並修正。
```

```prompt [label="無效的提問範例"]
幫我修 bug
```

### ⌨️ 常用快捷鍵與指令

| 操作       | 說明                         |
| ---------- | ---------------------------- |
| `/help`    | 查看所有可用指令             |
| `/clear`   | 清除對話記錄（節省 context） |
| `/compact` | 壓縮對話記錄保留摘要         |
| `Escape`   | 中斷當前執行中的任務         |
| `Ctrl+C`   | 完全退出 Claude Code         |

### 🔧 Plan Mode vs Auto Mode

[tags]
- [blue] Plan Mode：AI 先列出執行計畫，等你確認後才動作
- [green] Auto Mode：AI 自動完成任務，適合信任度高的操作
- [orange] 建議：新手多用 Plan Mode，熟悉後再開放 Auto
[/tags]

```prompt [label="啟用 Plan Mode"]
/plan
請重構 utils/formatter.ts，讓函式更易讀
```

## 讀寫檔案與執行指令

### 📁 讓 AI 理解你的專案

```prompt [label="理解專案結構"]
幫我了解這個專案的架構，重點說明：
1. 資料夾結構與用途
2. 主要的資料流向
3. 我應該先從哪個檔案開始看
```

```prompt [label="快速新增功能"]
在 src/components/ 新增一個 UserCard 元件：
- 顯示用戶頭像、名稱、email
- 使用 TypeScript interface 定義 props
- 符合現有專案的 CSS 風格（參考 ProductCard.tsx）
```

> **AI 看得到你的整個專案**
> 不需要複製貼上程式碼到對話框。Claude Code 直接讀取檔案，理解上下文後再回應，比任何 web 版 AI 工具都更準確。

### 🚀 執行指令的正確姿勢
- 告訴 AI 你的目的，讓它選擇適合的指令
- 需要多步驟時，描述完整流程
- 遇到錯誤，直接讓 AI 看錯誤訊息並修正

```prompt [label="自動化部署流程"]
幫我完成以下流程：
1. 執行測試，確認全部通過
2. Build 專案
3. 提交變更並推送到 main 分支
如果任何步驟失敗，停下來告訴我原因
```

---

# 客製化你的 Claude：打造專屬工作流
> 預設的 Claude Code 是通用的，但配置過的 Claude Code 是你的

## CLAUDE.md — 給 AI 的專案說明書

### 📋 CLAUDE.md 的作用
- Claude Code 每次啟動都會讀取 `CLAUDE.md`
- 用來告訴 AI：這個專案的規則、架構、慣例
- 沒有 CLAUDE.md 的專案，等於讓 AI 每次都重新摸索

```prompt [label="初始化 CLAUDE.md"]
/init
```

### ✍️ CLAUDE.md 應該寫什麼？

[flow]
1. 專案簡介 — 這是什麼系統、給誰用的
2. 技術棧 — 主要框架、語言、工具
3. 開發慣例 — 命名規則、資料夾結構
4. 注意事項 — 禁止修改的檔案、已知的特殊邏輯
[/flow]

> **CLAUDE.md 是一次性投資，長期受益**
> 每次開新對話，AI 都會讀取這份說明書。寫好一次，之後每次互動都更精準、更省 context。

### 💡 CLAUDE.md 範例片段

```prompt [label="CLAUDE.md 範例"]
# 專案說明
這是一個電商後台管理系統，使用者為公司內部員工。

## 技術棧
- Frontend: React + TypeScript + TailwindCSS
- Backend: Node.js + Express + PostgreSQL
- 測試: Jest + Testing Library

## 開發規範
- 所有 API 回應需符合 src/types/api.ts 定義的格式
- 新功能必須附帶單元測試
- 禁止直接修改 migrations/ 資料夾中已執行的 migration
```

## Agent Skills — 讓 AI 掌握你的工作方式

### 🎯 什麼是 Agent Skills？
- 放在 `.claude/skills/` 的 Markdown 檔案
- 描述特定任務的執行流程、規則、範例
- Claude Code 依情境自動讀取並應用

```prompt [label="建立 Skill 的 Prompt"]
幫我建立一個 git-commit Skill：
- 分析變更內容，自動判斷應分幾個 commit
- commit 訊息格式：type(scope): description
- 中文說明，英文 commit message
```

### 📦 常見的 Skill 應用場景

[tags]
- [green] git-commit：規範化 commit 訊息，自動分析變更
- [blue] code-review：按照團隊標準審查程式碼
- [purple] test-generator：根據函式自動生成測試案例
- [orange] deploy：標準化部署流程，減少人為錯誤
[/tags]

> **Skill 的本質是「把你的知識教給 AI」**
> 工作了幾年，你知道什麼是好的 commit、什麼是好的 code review。把這些隱性知識寫成 Skill，讓 AI 每次都按照你的標準執行。

## Memory — 讓 Claude 記住你

### 🧠 Claude Code 的記憶系統
- **Project Memory**：CLAUDE.md，對整個專案生效
- **User Memory**：`~/.claude/CLAUDE.md`，對所有專案生效
- **Conversation Memory**：對話中的上下文，關掉就消失

```prompt [label="儲存偏好設定"]
記住：我喜歡簡短的程式碼回覆，不需要解釋，直接給我修改好的版本
```

### 🔄 如何建立持久記憶？

[flow]
1. 在對話中說出偏好或規則
2. 要求 Claude 儲存到 CLAUDE.md 或 User Memory
3. 之後的對話會自動套用
[/flow]

---

# 實戰應用：讓 Claude Code 融入你的工作
> 工具用得好不好，差別在有沒有找到對的場景

## 開發場景實戰

### 🐛 除錯（Debug）

```prompt [label="系統性除錯"]
這個函式回傳的結果不對，預期是 [1, 2, 3]，實際是 [1, 2, 2]。
請：
1. 分析可能的原因
2. 加入 console.log 追蹤資料流
3. 找到問題後直接修正並移除 debug log
```

### 🏗️ 重構（Refactor）

```prompt [label="安全重構"]
重構 src/utils/dataProcessor.ts：
- 將超過 50 行的函式拆分
- 加入 TypeScript 型別
- 不要改變函式的行為，只改善可讀性
- 重構完成後執行現有測試確認沒有破壞
```

### 📚 理解陌生程式碼

```prompt [label="快速上手陌生專案"]
我剛接手這個專案，請幫我：
1. 解釋 src/core/engine.ts 的核心邏輯
2. 畫出主要函式的呼叫關係
3. 指出我需要特別注意的地方
```

## 避免常見陷阱

### ⚠️ 新手常犯的錯誤

[flow]
1. 問題太模糊 → AI 猜測方向，容易跑偏
2. 一次改太多 → 出錯時難以定位問題
3. 不驗證結果 → AI 的修改可能引入新 bug
4. 忽略 Plan Mode → 讓 AI 直接動作，錯了再回頭
[/flow]

> **AI 越強，你的判斷越重要**
> Claude Code 能做的事情很多，但最後按下「確認」的是你。不要因為 AI 說得很有自信就跳過驗證 — 自信不等於正確。

### ✅ 好習慣養成

- [x] 每次對話前清楚說明目標與限制
- [x] 大改動前先進入 Plan Mode 確認方向
- [x] 完成後跑測試，確認沒有 regression
- [x] 重要的工作流程寫成 Skill，建立護城河

### 💡 善用 Context Window

```prompt [label="清理 Context 的時機"]
/clear
```

- 換主題時清除對話（避免 AI 被舊資訊干擾）
- 感覺 AI 開始「記錯事情」時清除
- 使用 `/compact` 保留摘要但釋放空間

## 建立個人工作流

### 🎯 從小處開始，逐步擴展

[flow]
1. 第一週：用 Claude Code 解決一個你每天都在做的重複任務
2. 第二週：建立第一個 Skill，固化你的工作方式
3. 第三週：把 CLAUDE.md 完善，讓每個對話都更準確
4. 第四週：嘗試讓 AI 獨立完成一個完整功能
[/flow]

> **學習 AI 工具不是搜集技巧，而是改變工作習慣**
> 每個工程師用 Claude Code 的方式都不同，因為每個人的工作情境都不同。找到最適合你的那條路，比學會所有功能更重要。

---

# 總結

[summary]
- 🤖 **認識 Claude Code** | AI 不只補全程式碼，而是真正能讀寫檔案、執行指令的開發夥伴
- ⚡ **核心操作** | 掌握對話技巧、Plan Mode、指令操作，讓每次互動都高效精準
- 🔧 **客製化工作流** | 透過 CLAUDE.md、Agent Skills、Memory 系統，打造專屬你的 AI 助手
- 🚀 **實戰應用** | 從除錯到重構，找到適合自己的應用場景，建立可持續的開發習慣
[/summary]
