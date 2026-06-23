# privacy-lgt

集中託管 lgt 旗下所有 iOS App 隱私政策的**純靜態站**,部署於 Cloudflare Pages,
對外網域為 **[privacy.lgt.wtf](https://privacy.lgt.wtf)**。

零 build、零依賴、零 framework。每份政策都是單一自足的 HTML(inline CSS、無外部
資源),確保法律文件長期穩定可訪問。

## URL 結構

Cloudflare Pages 把資料夾結構直接映射為 URL:

| 路徑 | 對應檔案 |
|---|---|
| `privacy.lgt.wtf/` | `index.html`(根頁,列出各 App) |
| `privacy.lgt.wtf/<app-slug>` | `<app-slug>/index.html` |

`<app-slug>` 用小寫 kebab-case。`_template/` 以底線開頭,**不會**被部署為公開路由。

## 結構

```
privacy-lgt/
├── CLAUDE.md                    # 給 LLM 的主入口(用途、流程、外部專案使用指引)
├── SPEC.md                      # 隱私政策內容契約(10 個必備 section + 驗收清單)
├── index.html                   # 根著陸頁
├── _template/
│   └── privacy-template.html    # 參數化母版
├── loot-lab/index.html          # 範例(遊戲類:有 SDK / 追蹤)
└── reel/index.html              # 範例(隱私優先:資料僅存裝置)
```

## 新增一款 App 政策

1. 以 `_template/privacy-template.html` 為基礎,依 `SPEC.md` 填好所有 `{{...}}` 參數
   (反映該 App **實際**的資料行為)。
2. 存為 `<app-slug>/index.html`。
3. 在根頁 `index.html` 的清單加上連結。
4. `git add . && git commit && git push` — Cloudflare Pages 自動部署。

> 也可由其他 App 專案的 LLM 產生:讓它讀 `SPEC.md` 與 `_template/privacy-template.html`,
> 結合該 App 的隱私事實,回傳填好的完整 HTML。詳見 [`CLAUDE.md`](./CLAUDE.md)。

## 部署(Cloudflare Pages)

1. Dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**,
   選此 repo。
2. Build 設定全部留空:Framework preset `None`、Build command 留空、
   Output directory `/`。
3. **Custom domains** 加上 `privacy.lgt.wtf`。

## 免責聲明

本 repo 的範本與範例為**一般性參考,非法律意見**。每份政策需準確反映該 App 實際的
資料行為,並依當地法規與實際情況調整。
