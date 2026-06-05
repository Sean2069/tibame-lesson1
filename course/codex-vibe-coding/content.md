# 為什麼不用 PPT：用 Vibe Coding 打造講義網頁
> 與其用傳統 PPT 做講義，不如讓 AI 幫你建立一個可量身打造的講義網站

## 這次課程的起源

### 💡 靈光乍現的備課實驗
- 受 Cake 邀請在台大分享「如何把 AI 導入工程師日常開發工作流」
- 備課時突然想到：既然課程在講 AI 寫程式，何不用 Vibe Coding 建講義網站？
- 花了一個晚上完成模板雛形設計
- 結果不僅可在電腦、平板、手機瀏覽，甚至還可以匯出 PDF

### 🌟 自製講義網站的優勢
- 使用者介面可完全根據自己的需求量身打造
- 封裝成 Agent Skill 後，只要提供講義初稿，AI 就會自動生成
- 對生成結果不滿意，可以調整 Markdown 文件修改細節

### 🔧 今天使用的工具
- **AI Agent**：ChatGPT 的 Codex（目前可免費使用）
- **程式碼編輯器**：任意編輯器（VSCode、Cursor、Antigravity 皆可）
- 展示兩種操作方式：終端機指令 vs 編輯器外掛

> **培養多個 AI 工具使用的能力**
> 我教學的目標從來不是強調哪一款工具最強，而是透過實際案例讓大家了解如何解決痛點。工具間的差異沒有你想像的那麼大；唯一要提醒的，就是不要為了折扣付年費。

---

# 安裝 Codex，在終端機生成網頁
> 從環境設定到生成第一個課程網頁，讓你在終端機中體驗 AI Coding Agent 的魅力

## 環境準備

### ⚙️ 確認 Node.js 版本

[flow]
1. 打開終端機，輸入 `node -v` 確認是否安裝
2. 若無版號，需先安裝 Node.js（建議透過 NVM 管理版本）
3. 安裝完成後輸入 `nvm -v` 確認
4. 輸入 `nvm install --lts` 安裝最新版 Node.js
[/flow]

```prompt [label="Mac 安裝 NVM"]
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
```

```prompt [label="確認 Node.js 版本"]
node -v
```

- Windows 用戶：下載 exe 安裝 https://github.com/coreybutler/nvm-windows/releases
- NVM 優勢：可快速在不同 Node.js 版本間切換、更新

### 📦 安裝 Codex

```prompt [label="全局安裝 Codex"]
npm i -g @openai/codex
```

### 🔐 三種登入方式

[tags]
- [green] 方案一（推薦）：透過 ChatGPT 帳號登入 — 取得認證網址後登入即可
- [blue] 方案二：無瀏覽器環境登入 — 在其他裝置輸入驗證碼（需先到 ChatGPT 設定啟用「Codex 裝置代碼授權」）
- [orange] 方案三：輸入 OpenAPI Key — 按用量計費，注意設定用量限制避免帳單超支
[/tags]

## 在終端機生成網頁

### 🎯 第一個 Prompt：生成課程講義網頁

```prompt [label="生成課程講義網頁"]
請扮演熟悉 AI 主題授課的講師，以「Agent Skills」為主題設計講義
講義用純 html 網頁（CSS/JS 都放裡面）呈現
日系風格的設計感，部分文字與背景可以搭配適當的漸層
開頭會根據內容呈現標題，然後下面有發人深省的標語
會根據不同層級與意圖呈現對應的區塊（ex: 大小標題、陳述、列點、流程）
最後放上社群連結鼓勵大家訂閱（FB/YouTube/Medium）
側邊欄會有對應的目錄，方便跳轉到對應位置
```

### 💡 Prompt 設計三要素

[flow]
1. **目標**：明確定義只生成純 HTML 網頁（方便日後部署）
2. **風格**：說明想要的設計風格，也可讓 AI 扮演設計師幫你想
3. **架構**：分階段提出網頁架構需求（開頭呈現、層級設計、社群連結、目錄）
[/flow]

### ⚠️ 第一版的現實

- 初步完成度其實已不錯，如果只想要「看起來可以用」的講義，做到這步就夠了
- 但如果你是追求細節的人，很快就會遇到問題：AI 生成的描述可能不符合期待，段落結構也未必是你要的

[tags]
- [blue] 方案一：與 AI 對話調整細節（隨機性太高，可能動到不該動的）
- [blue] 方案二：直接修改 HTML（就算是工程師，改起來都覺得痛苦）
[/tags]

> **生成速度再快、畫面再漂亮，都是假的**
> 假使初始版本在後續要花很大力氣才能調整，它很難應用到現實情境中。我們需要換一種思路。

---

# 用 Vibe Coding 建立可重複使用的模板
> 讓 AI 每次都從穩定的基礎出發，而不是從零開始猜測你想要什麼

## 模板設計思維

### 🏗️ 為什麼需要模板？
- 生成式 AI 的輸出注定充滿隨機性
- 模板核心概念：不讓 AI 每次都從零開始生成，而是建立一套可放入不同內容的框架
- 適用範圍廣：簡報、文件、網頁，只要是重複性的工作都可套用
- 實際案例：受邀企業內訓時，有了模板只要替換內容，就能快速產出符合需求的講義

### 🔄 從 HTML 逆向到 Markdown

```prompt [label="建立 Markdown 可編輯模板"]
我希望剛剛生成出來的網頁，是可以透過 Markdown 格式編輯內容的
請幫我將網頁結構拆解（列點、步驟、圖片、表格、註解）、分層次（大標、中標、小標），並以常見的 Markdown 語法來設計規則
最後建立一個腳本，我只要編輯 Markdown 文件，網頁的 HTML 就會及時改變
操作方式寫在 README.md 文件中，並建立 package.json
```

[flow]
1. **期待目標**：網頁可透過 Markdown 格式編輯
2. **設計架構**：拆解網頁結構、分層次、設計 Markdown 語法規則
3. **渲染方式**：建立腳本，Markdown 文件修改後 HTML 即時改變
4. **說明文件**：操作方式寫入 README.md，建立 package.json
[/flow]

> **把內容放在可編輯的格式中，而不是最終輸出的 HTML 裡**
> 想要對內容有掌控力，就應該設計在方便維護的格式中。這樣才能讓 AI 幫你快速建立第一版，你再輕鬆調整細節。

## 建立 Agent Skill 工作流

### 🤖 封裝成可重複使用的 Agent Skill

```prompt [label="建立 Agent Skill"]
根據下面需求在「.agents」資料夾建立 Skill：
- 參考模板：根據剛剛腳本設計的規格，建立明確的 Markdown 使用規範
- 觸發時機：使用者提供初步想法想建立網頁時，會觸發這個 Skill
- 執行順序：這個 Skill 會先深入研究輸入的主題，再根據規範設計對應的 Markdown 文件；最後把 Markdown 文件透過腳本生成 html
- 特別提醒：預計會有多個主題，所以觸發時，請先建立新的資料夾，裡面存放新生成的 Markdown 與 HTML 檔案；並且建立獨立的 scripts 與 references 資料夾，確保可單獨執行
```

### 📁 Agent Skill 結構說明
- `.agents` 資料夾中包含 `SKILL.md` 檔案
- `name`：Skill 的名稱
- `description`：說明觸發的時機點與預計的執行成果
- `references/`：存放 Markdown 格式的參考文件
- `scripts/`：存放模板編譯的程式腳本

## 安裝 Codex 外掛

### 🔌 在編輯器安裝 Codex 外掛

[flow]
1. 點擊左側 Extensions，輸入「chatgpt」
2. 找到第一個外掛並安裝
3. 若找不到，在網址列輸入 `antigravity:extension/openai.chatgpt`
4. 安裝完成後打開任一文件，點擊上方 ChatGPT 圖示
5. 點擊「Setting」按鈕，選擇登入 ChatGPT 帳號
[/flow]

### 🖥️ Codex 外掛介面功能

[tags]
- [blue] 模型切換：輕鬆切換 GPT 模型與調整思考深度
- [green] 滑鼠符號：讓 AI 辨識你目前選中的區域和打開的檔案
- [purple] /plan：啟用 Plan Mode，獲得更詳盡的規劃
- [orange] /status：確認目前剩餘的使用額度
[/tags]

### ✅ 驗證 Agent Skill 效果

```prompt [label="從主題生成講義"]
我想要建立深度介紹「ChatGPT 使用技巧」的課程講義網頁。
```

```prompt [label="從草稿轉換講義"]
轉換成網頁，並啟動專案
```

---

# 成果展示與進階設定
> 從成品展示到部署技巧，了解自建模板的真實樣貌

## 模板功能展示

### 🌟 已實現的功能

[tags]
- [green] 側邊欄可自由收合，收合後顯示授課進度條
- [green] 指令旁有一鍵複製 icon（單手即可操作）
- [green] 自由切換淺色 / 深色模式，多款主題可選
- [green] 中場休息功能，含倒數計時
- [green] 優化的 PDF 匯出版面（非直接列印網頁）
- [green] 簡報模式（全螢幕呈現）
[/tags]

### ⚠️ 自建模板的代價
- 模板的細節需要在實際使用後，才知道哪裡要調整
- 設計與程式撰寫可以交給 AI，但方向與美感還是要自己掌握
- 市面上已有很多線上簡報工具，自建模板是為了最符合自己需求

> **你想要主控權，就得承擔客製化背後的複雜度**
> 這不是建立一個更好的方案，而是設計一套最符合自己需求的工具。

## 部署與進階設定

### 🚀 部署到 GitHub Pages

[flow]
1. 打開 Source Control，選擇 Init Repository，選擇 Public
2. 點擊 Generate 自動生成 commit 並 Push Branch 到 GitHub
3. 到 GitHub Settings → Pages
4. 選擇 Deploy from a branch，把 Branch 切換到 main
5. 到 Actions 頁面確認部署完成，取得網址
[/flow]

### 🔍 OG 設定（Open Graph）
- 打算公開分享時，必須設定 title、description、image
- 沒有 OG 設定，社群平台的網址預覽會顯示空白或錯誤縮圖
- 可到 `https://www.opengraph.xyz/` 貼上網址確認設定是否完整

### 📦 共用資訊的系統設計

[flow]
1. 講者資訊、頁尾社群宣傳 → 抽出放到 `global.yaml` 共用
2. OG 圖片 → 放在 `assets` 資料夾統一管理
3. 課程客製化資訊 → 個別 `config.yaml` 覆蓋全域設定
4. 變動性高的講稿內容 → Markdown 文件方便修改
[/flow]

> **用系統設計角度思考模板，才能讓它越用越好**
> 我已經用 AI 寫了 3 年多的程式，最大的感觸是：當我們開始思考專案架構的時候，Vibe Coding 的成果才會慢慢脫離 Demo，進入長期可用的狀態。

---

# 結語
> 知道自己要什麼，然後動手做就對了

[summary]
- 🌐 **從零生成課程網頁** | 終端機輸入一段 Prompt，幾分鐘內完成課程講義網頁
- 📝 **打造 Markdown 維護的模板** | 把 AI 的隨機輸出，轉成可用 Markdown 維護的穩定模板
- 🤖 **封裝成 Agent Skill** | 把模板打包成可重複使用的 Skill，讓 AI 每次都能快速產出
- 🏗️ **系統設計思維** | Vibe Coding 從玩具走向產品，關鍵在開始思考架構與長期維護
[/summary]
