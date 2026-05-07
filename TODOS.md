# TODOS

Captured items deferred from `/plan-eng-review` for Vwake VTuber 上架落地頁(2026-05-07)。

---

## 1. 詢問表單升級 — 從 mailto: 改為 web 表單

**What:** 把 `/vwake/` 與 `/en/vwake/` 的 CTA 從 `mailto:contact@hocatech.com` 升級為 web 表單(候選工具:Formspree / Tally / Google Form / 自建)。

**Why:** mailto: 在使用者沒有預設 mail client 時會 silent fail。VTuber 在公司電腦、iPad、學校網路下點擊可能完全沒反應 — 是隱形漏斗流失。

**Pros:**
- 保證詢問訊息一定送達(無 mail client 也能填)
- 後台可看到歷史詢問列表
- 可加自訂欄位(頻道規模、平台、上架時間期望)
- 表單填寫率通常比 mailto: 高 2-3x

**Cons:**
- Formspree/Tally 免費版有量上限(超過要付月費)
- 自建需要 backend(目前是純靜態,要引入新 stack)
- 多一個 3rd party dep(穩定性、隱私政策更新)

**Context:** 設計文件 `~/.gstack/projects/poter135-hocatech-website/poter-main-design-20260507-113959.md` Open Question #3 已列。決策節點:等收到第一輪 VTuber mailto: 詢問後,看實際數量與「明顯有人想填但 mailto: 失敗」的訊號,再決定升級時機。

**Depends on:** 先收 1-2 週 mailto: 詢問數據。

---

## 2. Open Graph / Twitter Card / schema.org SEO meta 補齊

**What:** 在 `/vwake/index.html` 與 `/en/vwake/index.html` 的 `<head>` 加 og:title / og:description / og:image / og:url / twitter:card / twitter:image,以及 schema.org Product 或 WebPage JSON-LD。

**Why:** VTuber 把 `/vwake/` 連結貼到 Twitter / Discord / LINE 時,預覽卡片(Open Graph)會影響其他人是否點擊。預設 fallback 只有 title + description,看起來像普通連結。設計過的 og:image 會讓分享變成「看一眼就懂」的廣告位。這是社群擴散的關鍵 — VTuber 跨座(向其他 VTuber 推薦)時,預覽卡決定點擊率。

**Pros:**
- 社群分享點擊率提升 2-5x
- 在 Discord / Twitter / LINE preview 變成品牌曝光
- schema.org 加分 SEO

**Cons:**
- 需要設計一張 1200x630 分享圖
- og:image 要 host 在絕對 URL(不能 relative)

**Context:** 1200x630 設計可以用 Vwake 的紫色漸層 + Vwake wordmark + 「讓你的聲音成為粉絲每天醒來的第一秒」tagline 做。可放在 `/vwake/og-image.png` 與 `/en/vwake/og-image.png`。

**Depends on:** 設計圖產出(Figma 或 CSS-to-PNG 工具)。

---

## 3. Asset 引入 — VTuber 頭像、App 截圖、demo 聲檔

**What:** 在頁面加入視覺資產:
1. Roster card 換掉「P」字佔位,改用 ぴょんちゃん 真實頭像(或 VTuber 提供的 Twitter avatar)
2. Hero 區加 Vwake App mockup 圖(可從 `Vwake/store_preview/page1.jpg` 取)
3. Pillar 2「整合」加 short GIF / video 顯示「在 App 內購買 → 立刻設為鬧鐘」流程
4. Roster card 加可試聽 audio sample(需 VTuber 同意公開,從 `Vwake/voice_packs_upload/` 取一段)

**Why:** 目前頁面**完全沒有任何 image / video / audio**。對 VTuber 圈來說,純 CSS 視覺看起來像「demo 還沒做好」。加上真實 asset 會讓「這個產品真的存在、真的有人在用」這個訊號變得無可懷疑。

**Pros:**
- 信任感 +50%(從「漂亮 landing page」變成「真實產品」)
- 可試聽是 conversion 引擎(VTuber 聽到品質 OK 才會願意上架)
- App mockup 對下載端粉絲也是預告

**Cons:**
- Page weight 從 ~30KB 變成 ~500KB-1MB(需 lazy load + WebP/AVIF + responsive image)
- Audio 需要小心 mobile autoplay 限制(只能 user-initiated 播放)
- 需要 VTuber 公開引用授權(Office hours Assignment 還沒做)

**Context:** 跟 Office hours Assignment(發信給 ぴょんちゃん 拿三句真話 + 公開引用授權)綁在一起。授權拿到後,asset 引入 + roster 文字更新 + 引言補上一次性處理。

**Depends on:**
- ぴょんちゃん 同意公開引用(前置)
- Vwake App 已上架 App Store / Google Play(下載按鈕才有意義)
- 1200x630 og:image 製作(TODO #2)
