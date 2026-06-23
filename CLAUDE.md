# CLAUDE.md — privacy-lgt 託管站主入口

這是一個**純靜態、零 build、零依賴**的 repo,集中託管 lgt 旗下所有 iOS App 的
隱私政策。部署在 **Cloudflare Pages**,對外網域為 **`privacy.lgt.wtf`**。

## URL 結構

Cloudflare Pages 把資料夾結構直接映射為 URL:

| 路徑 | 對應檔案 | 用途 |
|---|---|---|
| `privacy.lgt.wtf/` | `index.html` | 根頁,列出所有 App 政策連結 |
| `privacy.lgt.wtf/<app-slug>` | `<app-slug>/index.html` | 某 App 的隱私政策 |

- `<app-slug>` 用小寫 kebab-case(如 `loot-lab`、`reel`)。
- `_template/` 以底線開頭,**不會**被當成公開路由部署,僅作母版來源。

## Repo 結構

```
privacy-lgt/
├── CLAUDE.md                    # 本檔:給 LLM 的主入口
├── SPEC.md                      # 隱私政策內容契約(必讀)
├── index.html                   # 根著陸頁
├── _template/
│   └── privacy-template.html    # 參數化母版
├── loot-lab/index.html          # 範例
└── reel/index.html              # 範例
```

## 約束(務必遵守)

- **純靜態**:不得引入任何 build step、framework、套件管理、CI。
- 每份 HTML **單檔自足**:inline CSS,無外部資源依賴(法律文件需長期穩定可訪問)。
- 不是法律意見:每份文件底部保留「一般性範本,需依實際情況與當地法規調整」聲明。

---

## 任務 A:在「本 repo」新增一款 App 政策

當你在 **本 repo** 工作、被要求新增某 App 的政策時:

1. 讀 **`SPEC.md`**,掌握必備的 10 個 section 與撰寫要求。
2. 讀 **`_template/privacy-template.html`**,掌握 HTML 骨架與樣式。
3. 向使用者確認該 App 的實際隱私事實(蒐集哪些資料、用哪些 SDK、是否面向兒童、
   是否有帳號與刪除機制等)。
4. 以母版為基礎,把每個 `{{...}}` 參數替換為填好的內容(HTML 片段,例如 `<p>`、
   `<ul>`)。**不要留下任何未替換的參數標記。**
5. 存檔為 `<app-slug>/index.html`。
6. 提醒使用者 `git add . && git commit && git push`,Cloudflare Pages 會自動部署。

新增 App 後,同步在根頁 `index.html` 的清單加上該 App 的連結。

---

## 任務 B:外部專案 LLM 使用指引(重要)

> 適用情境:**你是某個 App 專案的 LLM**(不在本 repo 裡),被該專案的開發者要求
> 「產生這個 App 的隱私政策」。本 repo 是一份**可被讀取的契約**,請依下列步驟產出。

**步驟:**

1. **讀 `SPEC.md`** — 了解一份合格政策必須涵蓋哪些 section 與要求(對齊 Apple
   Privacy Nutrition Label、GDPR/CCPA/COPPA)。
2. **讀 `_template/privacy-template.html`** — 了解 HTML 骨架、section 結構與樣式。
   你的輸出必須沿用此骨架(相同的 section、相同的 inline 樣式風格)。
3. **結合該 App 的實際隱私事實**,逐一填寫所有 `{{...}}` 參數:
   - 蒐集哪些資料(對齊該 App 在 App Store Connect 的隱私問卷)
   - 用了哪些第三方 SDK / 服務及其用途
   - 是否面向或可能被兒童使用
   - 資料保留多久、使用者如何請求刪除
   - 聯絡信箱(預設 `privacy@lgt.wtf`,除非該 App 另有指定)
4. **回傳一份完整、已填好、可直接存檔的 HTML 檔**:
   - ✅ 單檔、inline CSS、無外部依賴
   - ✅ 所有 `{{...}}` 都已替換,無殘留參數
   - ❌ 不要回傳片段、Markdown、或「請自行填入」的待辦
   - 檔名建議:`<app-slug>/index.html`,放進本託管站即可上線
5. 跑一遍 SPEC.md 末尾的「產出檢查清單」自我驗收。

**核心提醒:政策必須準確反映該 App 自己的資料行為。不同 App 的隱私事實不同,
嚴禁照抄其他 App 的政策內容。** 寧可保守、誠實揭露,也不要寫出與實際行為不符的
描述(與 App Store Connect 問卷矛盾會被退件,與實際行為不符有法律風險)。

---

## 取得母版與契約的方式

外部 LLM 若能存取此 repo(已 clone 或經由 raw URL),直接讀取:
- `SPEC.md`
- `_template/privacy-template.html`

若僅能存取線上版,範例政策可參考 `https://privacy.lgt.wtf/loot-lab` 與
`https://privacy.lgt.wtf/reel` 的成品樣貌。
