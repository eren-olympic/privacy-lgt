# SPEC.md — 隱私政策內容契約

本文件定義一份「合格隱私政策」**必須涵蓋的 section 與撰寫要求**,目標是滿足
**Apple App Store 審核**(Guideline 5.1.1 等)以及一般性的 GDPR / CCPA / COPPA
合規期待。任何 App 的 LLM 在產生政策時,都應依本契約逐項填寫,確保不同 App
產出的結構一致、不漏項。

> ⚠️ 本契約與所附範本為**一般性參考**,非法律意見。最終文件需準確反映該 App
> 實際的資料行為,並依當地法規與實際情況調整。

---

## 撰寫總則

1. **準確第一**:政策必須如實描述該 App 實際蒐集、使用、分享的資料。
   不確定或不適用的項目,寧可明確寫「本 App 不蒐集 X」,也不要照抄別的 App。
2. **與 Apple Privacy Nutrition Label 對齊**:第 2 節的資料分類應與你在
   App Store Connect 填寫的「App 隱私」問卷一致,兩者矛盾會被退件。
3. **白話、具體**:避免空泛法律術語堆砌;說清楚「蒐集什麼、為什麼、給誰」。
4. **可獨立閱讀**:輸出為單一自足 HTML(inline CSS、無外部資源),長期穩定可訪問。
5. **填寫 `{{LAST_UPDATED}}`** 用 ISO 格式 `YYYY-MM-DD`。

---

## 必備 Sections

對應 `_template/privacy-template.html` 中的參數標記。每節說明用途與要求:

### 1. 簡介與適用範圍 — `{{INTRO}}`
- 一句話說明本政策適用於哪個 App(名稱)、由誰提供(開發者/個人或公司名)。
- 說明適用範圍:僅涵蓋此 App,不涵蓋第三方連結或服務。
- 點明使用者使用本 App 即表示已閱讀並理解本政策。

### 2. 蒐集的資料類型 — `{{DATA_TYPES}}`
- 逐類列出**實際蒐集**的資料,並對齊 Apple Privacy Nutrition Label 分類,常見類別:
  - Contact Info(姓名、Email、電話)
  - Health & Fitness
  - Financial Info(付款資訊、購買紀錄)
  - Location(精確/粗略)
  - Sensitive Info
  - Contacts(通訊錄)
  - User Content(照片、文字、檔案等使用者產生內容)
  - Browsing / Search History
  - Identifiers(User ID、Device ID、IDFA)
  - Usage Data(互動、瀏覽紀錄)
  - Diagnostics(崩潰資料、效能數據)
- **每一類都要區分**:是否與身分關聯(linked / not linked)、是否用於追蹤(tracking)。
- 若 App **完全不蒐集任何資料**,明確聲明,並說明資料(如有)僅留存在裝置本機。
- 說明資料來源:使用者主動提供 vs. 自動蒐集(感測器、log 等)。

### 3. 資料用途 — `{{DATA_USAGE}}`
- 逐項對應第 2 節的資料,說明用途。常見用途:
  - App 功能運作(核心功能所需)
  - 帳號管理與驗證
  - Analytics / 產品改善
  - 個人化內容或推薦
  - 廣告(若有)
  - 法律遵循
- 若有跨 App/跨網站**追蹤(tracking)**,需明確揭露,並對應 App Tracking Transparency(ATT)。

### 4. 第三方 SDK 與服務 — `{{SDK_LIST}}`
- 列出整合的第三方 SDK / 服務及其用途與資料行為,常見如:
  - Analytics:Firebase Analytics、Google Analytics、Mixpanel、Amplitude
  - 崩潰回報:Crashlytics、Sentry
  - 廣告:AdMob、Meta Audience Network
  - 後端 / 雲端:Firebase、Supabase、CloudKit、AWS
  - 登入:Sign in with Apple、Google Sign-In
  - 付款:Apple In-App Purchase、RevenueCat、Stripe
- 每個 SDK 標明:蒐集什麼、用途、並附上其隱私政策連結(若可)。
- 若**未使用任何第三方 SDK**,明確聲明。

### 5. 第三方資料分享 — `{{THIRD_PARTY_SHARING}}`
- 說明是否、以及在何種情況下將資料分享給第三方(服務供應商、廣告商、法律要求等)。
- 明確聲明**是否販售使用者資料**(CCPA 要求:多數情況應聲明「不販售」)。
- 區分「為提供服務而必要的處理者(processor)」與「對外揭露/販售」。

### 6. 資料保留與刪除 — `{{DATA_RETENTION}}`
- 說明資料保留多久、依何標準(達成目的即刪除 / 法定期限等)。
- **明確提供使用者刪除資料的方式**(Apple 要求帳號類 App 須提供 App 內帳號刪除):
  - App 內如何刪除帳號 / 資料
  - 或寄信至聯絡信箱請求刪除,及處理時程
- 若資料僅存於裝置本機,說明解除安裝即清除。

### 7. 使用者權利 — `{{USER_RIGHTS}}`
- 依適用法規列出使用者權利:
  - **GDPR**(歐盟):存取、更正、刪除、限制處理、可攜、反對、撤回同意。
  - **CCPA/CPRA**(加州):知情、刪除、選擇退出販售/分享、不受歧視。
- 說明如何行使這些權利(通常是聯絡信箱)。
- 視 App 受眾調整;若不確定適用範圍,採較保守(較完整)的揭露。

### 8. 兒童隱私 — `{{CHILDREN_CLAUSE}}`
- 依 App 受眾選擇對應寫法:
  - **非面向兒童**:聲明本 App 非為 13 歲(或當地法定年齡)以下兒童設計,不會
    刻意蒐集兒童個資;若發現誤蒐將刪除。
  - **面向兒童(Kids Category 或可能被兒童使用)**:需符合 **COPPA**,說明取得
    家長同意的機制、不投放行為廣告、限制資料蒐集等。
- COPPA 違規是 App 審核與法律的高風險區,務必如實。

### 9. 政策變更通知 — (範本已內建固定文字)
- 說明變更時如何通知(更新「Last updated」日期,重大變更於 App 內提示)。
- 範本已提供標準段落,通常無需 App 自訂,除非有特殊通知機制。

### 10. 聯絡方式 — `{{CONTACT_EMAIL}}`
- 預設 `privacy@lgt.wtf`。提供使用者就隱私問題聯絡的有效管道。

---

## 產出檢查清單(LLM 自我驗收)

- [ ] 10 個 section 全數填寫,無殘留 `{{...}}` 參數。
- [ ] 第 2 節資料類型與該 App 在 App Store Connect 的隱私問卷一致。
- [ ] 第 4 節列出所有實際整合的 SDK(或明確聲明無)。
- [ ] 第 6 節提供具體的刪除途徑(帳號類 App 須有 App 內刪除)。
- [ ] `{{LAST_UPDATED}}` 為 `YYYY-MM-DD`。
- [ ] 輸出為單一 HTML、inline CSS、無外部資源。
- [ ] 內容反映**該 App 自己的事實**,未照抄其他 App。
- [ ] 保留底部「非法律意見」聲明。
