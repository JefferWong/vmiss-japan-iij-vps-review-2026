# My VMISS Japan IIJ VPS Experience: Day-One Connectivity Failures, Rigid Support, and a 22.2% Refund Deduction

**Purchase date:** November 9, 2026  
**Service:** VMISS Japan IIJ VPS  
**Purchase price:** CAD 4.50  
**Status as of November 9, 2026:** VMISS offered a refund subject to a CAD 1.00 non-refundable fee. I requested a full fee waiver due to same-day failure; I have **not** accepted the partial deduction, and no refund has been completed. Rather than addressing my request, support's response was to unilaterally dismiss the inquiry and prepare to close the ticket.

> **Disclaimer:** This is a factual account of my individual purchase, poor network experience, and frustrating customer service interactions. The network measurements below describe my particular testing environment and routes on China Telecom. They do **not** prove that VMISS's entire network is globally defective, nor do they prove that the assigned IP was blocked. I have removed all sensitive account and connection details.

## TL;DR

I purchased a CAD 4.50 VMISS Japan IIJ VPS on November 9, 2026. The day-one out-of-the-box experience was dismal: my very first IPdog connectivity check failed immediately. Subsequent testing directly over a China Telecom connection revealed a 20% ICMP packet loss in a 30-packet sample, alongside severe, recurring TCP handshake latency spikes (~1.1 seconds) across multiple service ports.

Hoping for a constructive resolution, I reached out to VMISS support on the very day of purchase to request a courtesy IP replacement. Support's response was remarkably rigid, unhelpful, and confrontational from the start:
- **Deflecting fault:** Support deflected all responsibility by repeatedly stating that IIJ is an unoptimized budget line where poor speeds and packet loss are "expected," while trying to upsell me to their much more expensive `JP.TKY.TRI` plan.
- **Absurd fee structure:** They demanded a CAD 5.00 fee to change the IP—more than the entire monthly price of the VPS (CAD 4.50)—unless I could definitively prove the IP was blocked prior to delivery.
- **Uncompromising stance:** They flatly shut down further discussion by declaring this their **"final decision."**
- **Punitive refund terms:** When I requested a cancellation, VMISS offered a refund but insisted on retaining a CAD 1.00 transaction fee—a staggering **22.2% penalty** on a CAD 4.50 order that was unusable from day one.
- **Cold dismissal:** When I asked for a goodwill fee waiver for a same-day failure, support coldly responded: **“If you need no further assistance, I will go ahead and close this ticket. No reply is necessary.”**

This review is not about expecting premium network performance from a budget VPS. It is about **the unacceptable customer experience, a dysfunctional day-one service, and support's rigid, dismissive attitude toward a legitimate consumer complaint**.

## 1. What I measured

The following measurements were taken from my **Mac on a China Telecom connection**, directly to the Japan VPS, on November 9, 2026. The Mac's ClashX system proxy was not used for these raw TCP socket tests, and its TUN mode was disabled. Independent endpoint and routing traces confirmed a direct connection path. (Results from a secondary machine that traversed a local transparent proxy have been excluded to maintain absolute data integrity.)

| Check | Result | What it does / does not show |
| --- | --- | --- |
| Initial IPdog check | Connection failed on the first test, as reported at the time | A failed initial check; **not conclusive proof that the IP was blocked** |
| ICMP ping | 30 sent, 24 received (**20% packet loss**); average RTT about **106.9 ms** | A small ICMP sample on China Telecom; ICMP loss may differ from TCP loss |
| TCP connections | **60/60 succeeded** across Reality, VMess, and AnyTLS ports | The server was reachable by TCP during these specific test runs |
| TCP latency | Median around **116–117 ms** across the three ports | Typical baseline TCP connection latency |
| TCP outliers | **7/60** connections took **over 800 ms**; several spiked to around **1.1 seconds** | Intermittent severe initial connection delays, consistent with SYN packet loss and retransmission |

Server-side packet captures further confirmed the issue: during slow connections, the first SYN packet was observed on the VPS approximately one full second after the Mac initiated `connect()`, after which the VPS promptly answered with SYN-ACK. This demonstrates that the initial packet was lost or stalled in international transit, triggering the client's 1-second initial retransmission timer (RTO).

While budget transit inevitably involves jitter, experiencing immediate 20% packet loss and 1.1-second connection stalls within hours of purchase—followed by complete support indifference—created a thoroughly frustrating customer experience.

## 2. Support timeline

All events occurred on **November 9, 2026**. Messages below are summarized excerpts; verbatim quotes reflect support's exact wording:

1. **Same-day complaint & request for help:** I reported the initial IPdog failure, the 20% ping loss, and the frequent 1.1s TCP delays, politely requesting a one-time courtesy IP swap.
2. **Deflection and upselling:** VMISS refused to investigate, claiming that Japan IIJ is a non-optimized line and that packet loss and latency are normal. Instead of assisting, they pushed an upsell to the more expensive `JP.TKY.TRI` tier.
3. **Exorbitant replacement fee:** VMISS stated that a free change was granted only if the assigned IP was provably dead upon delivery. Otherwise, an IP replacement would cost **CAD 5.00**—exceeding the entire purchase price of CAD 4.50—with a mandatory **30-day** cooldown.
4. **Rigid stonewalling:** When I asked for management review, support doubled down on the non-optimized disclaimer, labeled their stance their **“final decision,”** and suggested closing the ticket.
5. **The 22.2% refund penalty:** VMISS subsequently stated that a refund would be subject to a **non-refundable CAD 1.00 fee** under their [refund policy](https://legal.vss.im/refund-policy.html), asking me to accept the deduction. On a CAD 4.50 purchase, this represents a **22.2% penalty** for returning an unusable service on day one.
6. **Request for a goodwill waiver:** I objected to paying a 22.2% penalty for a failed service reported within hours of purchase, requesting a full CAD 4.50 refund as a fair customer-service exception.
7. **Cold dismissal:** The support agent responded: **“If you need no further assistance, I will go ahead and close this ticket. No reply is necessary.”** My waiver request was ignored, and the communication was abruptly shut down.

## 3. Why the customer experience was unacceptable

- **Unusable on Day One:** Expecting basic connectivity from a newly provisioned VPS is not asking for "premium routing." When a service fails basic reachability tests on the day of delivery, treating the customer as unreasonable is unacceptable.
- **Deflection over Investigation:** Support made no effort to diagnose the problem or verify whether the IP had routing issues. They simply hid behind the "non-optimized" label.
- **Fee Inversion:** Demanding CAD 5.00 to replace an IP on a CAD 4.50 server is completely disproportionate. It punishes the buyer for receiving an unstable allocation.
- **Unreasonable Deduction on Micro-Transactions:** Enforcing a flat CAD 1.00 deduction on a CAD 4.50 order extracts a 22.2% fee from the customer. While VMISS relies on written policy terms, applying such fees to same-day service complaints shows zero commercial goodwill or flexibility.
- **Arrogant and Dismissive Attitude:** Citing "final decision" and ending a customer inquiry with *"No reply is necessary"* reflects a rigid, take-it-or-leave-it support culture that dismisses customer feedback once payment has been captured.

## 4. What I requested, and the outcome

I proposed two straightforward, reasonable remedies: **either** a one-time complimentary IP replacement **or** a full refund of **CAD 4.50** without the CAD 1.00 penalty.

VMISS rejected the IP swap and offered only the partial refund. **As of this publication, I have refused to accept the partial deduction, and no refund has been processed.**

My advice to prospective buyers: be fully aware of VMISS's rigid policies and unforgiving support attitude. If network reliability from your ISP matters, test thoroughly within the first hour, keep every log, and be prepared for zero flexibility if things go wrong.

## 5. Evidence and privacy

The following documentation has been archived and verified:
- Proof of purchase dated November 9, 2026, for **CAD 4.50** (account identifiers redacted).
- Contemporaneous test logs documenting the initial IPdog connection failure.
- Timestamped Mac ping, TCP socket latency metrics, and server-side packet captures.
- Complete ticket logs showing the exact exchanges, with personal identifying information redacted.

No passwords, UUIDs, private keys, subscription URLs, or unmasked IP addresses are published.

---

# 中文版｜VMISS 日本 IIJ VPS：購置當日連線嚴重異常、態度強硬消極與 22.2% 退款扣費爭議

**購買日期：** 2026 年 11 月 9 日  
**服務：** VMISS 日本 IIJ VPS  
**訂單金額：** 4.50 加元  
**截至 2026 年 11 月 9 日的狀態：** VMISS 提出退款但堅持扣除 1.00 加元不可退手續費。我已明確要求豁免，**尚未確認接受扣費退款，亦未收到退款已完成的確認**。客服最新回覆直接準備關閉工單，完全未實質回應豁免手續費之訴求。

> **說明：** 這是一篇記錄個人實際購買、極差連線體驗及消極售後服務的客觀經歷。網路量測數據僅對應我當時在中國電信網路下的測試環境與路由，**不能證明 VMISS 全網皆有問題，亦不能證明所配發的 IP 遭到封鎖**。公開內容已嚴格進行隱私脫敏。

## 一、事情經過

2026 年 11 月 9 日，我以 **4.50 加元** 購買了一台 VMISS 日本 IIJ VPS。開通後的實際體驗極度令人失望：開箱首次 IPdog 測試便直接報告連線失敗。隨後，我從 **中國電信網路的 Mac** 進行原始直連測試：30 次 ICMP Ping 遺失 6 次（**封包遺失率達 20%**）；三個 TCP 服務埠合計 60 次交錯連線測試中，雖全部成功，但竟有 **7 次耗時超過 800ms**，其中多次出現長達 **1.1 秒** 的嚴重卡頓。

作為當日剛付費的消費者，我在第一時間向 VMISS 提出申訴，希望在保留既有配置的前提下獲得一次免費更換 IP 的合理善後。然而，客服從一開始便展現出極其僵化、推諉且強硬的態度：
- **推諉線路品質：** 客服一再強調 IIJ 是非優化便宜線路，連線延遲與丟包屬於「正常現象」，並反向推銷更昂貴的 `JP.TKY.TRI` 方案。
- **荒謬的收費門檻：** 聲稱除非能證實初始 IP 在交付當下即被封鎖，否則更換 IP 必須額外支付 **5.00 加元**（竟比整台伺服器一個月的租金 4.50 加元還要貴！），且規定換 IP 間隔須滿 30 天。
- **拒絕溝通的「最終決定」：** 在進一步交涉中，客服強硬宣稱這就是他們的 **「最終決定（final decision）」**，甚至主動提議直接關閉工單。
- **高達 22.2% 的退款手續費剝削：** 在後續退款溝通中，客服表示退款必須扣除 **1.00 加元手續費**。對於一筆當天購買、因連線品質惡劣而無法正常使用、總價僅 4.50 加元的微額訂單，1 加元的扣費比例高達 **22.2%**！
- **冷漠送客的消極態度：** 當我提出身為新購當日報障個案，應給予善意全額退款時，客服的最新回覆竟是冷冰冰地下達逐客令：**「若無其他需要，我將直接關閉此工單，您無需回覆。」** 完全拒絕正視客戶提出的訴求。

## 二、測試證據與邊界

| 測試項目 | 結果 | 注意事項 |
| --- | --- | --- |
| 首次 IPdog 測試 | 報告連線失敗 | **不能僅憑單次結果認定 IP 遭到封鎖** |
| 中國電信 ICMP Ping | 發出 30 次，收到 24 次，**封包遺失率 20%**；平均 RTT 約 **106.9ms** | 樣本較小，ICMP 封包遺失不等於 TCP 封包遺失 |
| 三個連接埠 TCP 連線 | **60/60 成功** | 說明測試當下 TCP 仍可連通，並非完全中斷 |
| TCP 典型建連延遲 | 各連接埠中位數約 **116–117ms** | 為底層 TCP 三向交握時間，非 ClashX 應用層代理測速 |
| TCP 長尾異常延遲 | **7/60 次超過 800ms**，多次集中於 **1.1 秒** | 與 SYN 超時重傳特徵高度吻合，證明出境連線存在隨機丟包 |

這組測試在 Mac 上透過原生 Socket 直連進行，ClashX 的 TUN 模式已關閉；另有路由及伺服器端封包擷取記錄支持其屬於純直連鏈路。**Windows 端因受本機網路環境影響，已嚴格剔除，避免干擾原始客觀數據。**

伺服器端抓包亦完整記錄了慢連線現場：Mac 發起 `connect()` 約 1 秒後，伺服器才首次接收到 SYN 封包，隨後迅速回覆 SYN-ACK。此現象確鑿證實了首個 SYN 封包在中途國際鏈路遭到丟棄，因而觸發了用戶端作業系統 1 秒的初始重傳計時器（RTO）。

## 三、為什麼我不滿意：糟糕的客戶體驗與強硬態度

- **開箱即遇故障，何來正常體驗：** 消費者購買服務，最基本的要求是開箱即用。新購當日便遭遇連線失敗與高達 20% 丟包，業者非但不主動排查，反倒責怪客戶購買了便宜線路，本末倒置。
- **推諉卸責，毫無技術診斷誠意：** 面對客觀測試數據，客服自始至終未提供任何線路診斷或技術說明，僅是一味機械式重複「非優化」說辭來敷衍塞責。
- **費用倒掛的荒唐條款：** 一台月租 4.50 加元的伺服器，要求客戶支付 5.00 加元去更換有瑕疵的分配 IP，毫無商業合理性可言。
- **22.2% 退款手續費極度嚴苛：** 針對購買當日即報障退訂的微額訂單，堅持扣取 1.00 加元手續費，扣款比例高達 22.2%。即便政策有寫，在面對服務無法正常交付的個案時仍強硬執行，顯得極度缺乏善意與商業彈性。
- **傲慢冷漠的售後溝通：** 在溝通中動輒以「最終決定」壓制客戶，最後甚至以「直接關閉工單、無需回覆」粗暴終止對話，展現出典型且惡劣的強硬傲慢姿態。

## 四、我的訴求與當前結果

我提出過兩種合情合理的解決方案：**免費更換一次正常可用之 IP**，或者**全額退還 4.50 加元且豁免 1 加元手續費**。

VMISS 斷然拒絕免費更換 IP，並強硬堅持扣費退款。**截至本文發布前，我並未同意該扣費退款方案，亦未聲稱退款已經完成。**

我寫下這段真實經歷，是希望提醒其他潛在買家：在選擇 VMISS 廉價 VPS 前，務必看清其極度嚴苛的換 IP 與退款政策，並對其強硬、消極的客服風格做好心理準備；若在意連線品質，請務必在開通第一時間完成實測並保存所有證據。

## 五、證據與隱私保護

擬備查的佐證資料包括：訂單日期與 4.50 加元金額憑證、最初 IPdog 失敗紀錄、Mac 測試日誌與伺服器端抓包記錄、經脫敏之客服工單完整截圖。

發布前已嚴格剔除所有密碼、UUID、API Token、證書私鑰、SSH 憑據、個人電子郵件及未脫敏之真實 IP 位址。
