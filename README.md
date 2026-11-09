# My VMISS Japan IIJ VPS Experience: Day-One Connectivity Issues and a 22.2% Refund Deduction

**Purchase date:** November 9, 2026  
**Service:** VMISS Japan IIJ VPS  
**Purchase price:** CAD 4.50  
**Status as of November 9, 2026:** VMISS offered a refund subject to a CAD 1.00 non-refundable fee. I requested a fee waiver; I have **not** confirmed acceptance of the partial refund, and I have not received confirmation of a completed refund. The support agent's latest reply suggested closing the ticket without addressing that request.

> **Disclaimer:** This is a factual account of my individual purchase and support experience. The network measurements below describe my particular testing locations, times, and routes. They do **not** prove that VMISS's entire network is unreliable, or that the assigned IP was blocked. I have removed sensitive account and connection details.

## TL;DR

I bought a CAD 4.50 VMISS Japan IIJ VPS on November 9, 2026. My first IPdog connectivity check reported a connection failure. Follow-up testing from a Beijing China Telecom connection showed 20% ICMP packet loss in a 30-packet sample, and intermittent slow TCP handshakes across three ports. I asked for a complimentary IP replacement on the day of purchase.

Support replied that the IIJ plan was not a premium route, that occasional loss could be expected, and that an IP replacement would cost CAD 5.00 unless the assigned IP was blocked at initial provisioning. After several exchanges, support described this as its **“final decision.”** Later, VMISS offered to refund the order but proposed retaining CAD 1.00 in fees—**22.2% of the CAD 4.50 purchase price**. When I requested a full refund as a goodwill exception, the latest reply was essentially an invitation to close the ticket.

The issue I want to highlight is not that a budget VPS should perform like a premium network. It is **how a same-day connectivity complaint and a small refund were handled**.

## 1. What I measured

The following measurements were taken from my **Mac on a Beijing China Telecom connection**, directly to the Japan VPS, on November 9, 2026. The Mac's ClashX system proxy was not used for these raw TCP socket tests; its TUN mode was disabled. Separate endpoint and routing checks supported direct connectivity. I am intentionally excluding Windows TCP results that were affected by a home-router transparent proxy.

| Check | Result | What it does / does not show |
| --- | --- | --- |
| Initial IPdog check | Connection failed on the first test, as reported at the time | A failed check; **not conclusive proof that the IP was blocked** |
| ICMP ping | 30 sent, 24 received (**20% loss**); average RTT about **106.9 ms** | A small ICMP sample; ICMP loss may differ from TCP loss |
| TCP connections | **60/60 succeeded** across Reality, VMess and AnyTLS ports | The server was reachable by TCP during these tests |
| TCP latency | Median around **116–117 ms** across the three ports | Typical initial TCP connection latency |
| TCP outliers | **7/60** connections took **over 800 ms**; several were around **1.1 seconds** | Intermittent slow initial connects, consistent with—but not definitive proof of—SYN retransmission |

I also collected server-side packet captures. A sample slow connection showed the first SYN observed on the VPS about one second after the Mac initiated `connect()`, followed by a prompt SYN-ACK from the VPS. This is consistent with a first-packet delay or retransmission somewhere along the path, but a server-only capture **cannot locate the point of loss**.

These results do not establish a contractual performance breach. They explain why I was dissatisfied with the connectivity from my network immediately after buying the service.

## 2. Support timeline

All events occurred on **November 9, 2026**. Messages below are abbreviated excerpts; the full original ticket can be provided in redacted screenshots.

1. **Same-day complaint.** I reported the initial IPdog failure, the ping loss, and the slow TCP connections, and requested a one-time free IP change while preserving the VPS setup.
2. **Non-premium routing explanation.** VMISS said the Japan IIJ plan was not a premium route and that occasional slow speeds or packet loss were normal. It recommended the more expensive `JP.TKY.TRI` series.
3. **Paid IP change policy.** VMISS stated that a free change was available only when an initially provisioned IP was blocked, and that other IP replacements cost **CAD 5.00**, with a **30-day** interval between changes.
4. **Final refusal.** VMISS reiterated the non-optimized routing disclaimer, described its position as its **“final decision,”** and offered to close the ticket.
5. **Refund offer.** VMISS subsequently said a refund would incur a **non-refundable CAD 1.00 transaction fee**, referencing its [refund policy](https://legal.vss.im/refund-policy.html), and asked me to confirm whether to proceed.
6. **Request to waive the fee.** I objected because CAD 1.00 is **22.2%** of a CAD 4.50 order purchased and disputed on the same day. I asked for a full CAD 4.50 refund as a one-time goodwill exception.
7. **Latest reply.** The agent replied: **“If you need no further assistance, I will go ahead and close this ticket. No reply is necessary.”** The message did not substantively address my request to waive the fee.

## 3. Why I am dissatisfied

- I **accept** that a non-optimized IIJ route may have higher latency and occasional loss. I was not asking for a premium-route guarantee.
- I reported a failed initial check and measurable connection instability **on the purchase date**. I had hoped for an actual review of whether a different IP or refund exception could reasonably be offered.
- The initial IPdog failure by itself does **not** prove that the IP was blocked at provisioning; equally, I was not shown a specific technical investigation of that question in the ticket responses I received.
- A **CAD 1.00 deduction on a CAD 4.50 order** feels disproportionate to me, especially for a same-day complaint. I recognize that VMISS cited its written refund policy; my objection is about customer-service discretion and fairness, not a proven finding of illegality.
- The final support messages felt dismissive, particularly after I requested management review and a fee waiver.

## 4. What I requested, and the outcome

I asked VMISS to consider **either** a one-time complimentary IP replacement **or** a full refund of **CAD 4.50** without the CAD 1.00 fee. VMISS declined the free IP replacement and offered a refund with the stated fee. **As of this write-up, I have not agreed to that partial-refund arrangement, and I am not claiming that a refund has been processed.**

My takeaway for other buyers: read the specific routing disclaimers and IP replacement/refund terms **before** purchasing a low-cost VPS. If performance from your ISP matters, test from your own network as early as possible and preserve the original measurements and support responses.

## 5. Evidence and privacy

I have retained, or can assemble from my records, the following supporting materials:

- Purchase confirmation showing the date and **CAD 4.50** price (account identifiers redacted).
- The original IPdog failure evidence **if available**; otherwise, the contemporaneous account of that failed check.
- Timestamped Mac ping/TCP results and relevant packet-capture excerpts.
- The support ticket messages, with account details, personal information, credentials, subscription links, and unrelated IPs redacted.

**No passwords, UUIDs, API tokens, private keys, subscription URLs, or unmasked personal IP addresses should be posted.** The VPS address is also masked in the public narrative because the service may still be active.

---

# 中文版｜VMISS 日本 IIJ VPS：购入当天连接异常与 22.2% 退款扣费争议

**购买日期：** 2026 年 11 月 9 日  
**服务：** VMISS 日本 IIJ VPS  
**订单金额：** 4.50 加元  
**截至 2026 年 11 月 9 日的状态：** VMISS 提出退款但扣除 1.00 加元不可退手续费。我已要求豁免，**尚未确认接受扣费退款，也没有收到退款已完成的确认**。客服最新回复表示若无其他需求将关闭工单，但未实质回应豁免费用的请求。

> **说明：** 这是一篇记录个人实际购买及售后体验的文章。网络数据仅对应我当时的测试地点、时间和路由，**不能证明 VMISS 全网均存在问题，也不能证明所分配的 IP 遭到封锁**。公开内容已尽量避免暴露账号和连接凭据。

## 一、事情经过

2026 年 11 月 9 日，我以 **4.50 加元**购买了一台 VMISS 日本 IIJ VPS。开通后的首次 IPdog 连接测试报告连接失败。随后，我从**北京电信网络的 Mac** 进行测试：30 次 ICMP Ping 丢失 6 次（**20%**），三个 TCP 端口合计 60 次连接虽然全部成功，但有 **7 次耗时超过 800ms**，其中多次约为 **1.1 秒**。

我在购买当天向 VMISS 请求免费更换一次 IP。客服强调该套餐属于非优化的 IIJ 线路，偶发延迟和丢包属于预期情况，并建议购买更昂贵的 `JP.TKY.TRI` 套餐。随后又说明，除非初始 IP 在交付时遭封锁，否则换 IP 需要 **5 加元**，两次换 IP 至少间隔 **30 天**。在进一步沟通中，客服表示这是他们的 **“最终决定”**。

后来客服提出可以退款，但要求扣除 **1 加元手续费**。对总价仅 **4.50 加元**的订单而言，这相当于 **22.2%** 的扣款。我请求作为新购当天报障的个案予以豁免，全额退还 4.50 加元。然而，最新回复只是表示可以关闭工单，并称“无需回复”，没有实质回应我的豁免请求。

## 二、测试证据与边界

| 测试项目 | 结果 | 注意事项 |
| --- | --- | --- |
| 首次 IPdog 测试 | 报告连接失败 | **不能仅凭这一结果认定 IP 被封锁** |
| 北京电信 ICMP Ping | 发出 30 次，收到 24 次，**丢包率 20%**；平均 RTT 约 **106.9ms** | 样本较小，ICMP 丢包不等于 TCP 丢包 |
| 三个端口 TCP 建连 | **60/60 成功** | 说明测试时 TCP 可连通，并非持续完全不可达 |
| TCP 典型建连时间 | 各端口中位数约 **116–117ms** | 为原始 TCP 建连时间，而非 ClashX 完整代理测速 |
| TCP 长尾 | **7/60 超过 800ms**，多次约 **1.1 秒** | 与 SYN 重传现象吻合，但不能仅凭这些数据精确定位丢包环节 |

这组测试在 Mac 上通过原生 Socket 进行，ClashX 的 TUN 已关闭；另有路由及服务端抓包记录支持其属于直连链路。**Windows 上访问同一日本节点的 TCP 测试受到家庭旁路由透明代理提前握手影响，因此没有混入上述原始直连数据。**

服务端抓包还曾显示一个慢连接：Mac 发起 `connect()` 后，服务端约一秒才首次看到 SYN，随后迅速回复 SYN-ACK。此现象支持链路存在首包延迟或重传的推测，但只凭服务器单端抓包不能确定丢包发生在哪个运营商节点。

## 三、为什么我不满意

我理解并接受廉价 IIJ 线路没有高端优化线路的稳定性保证。我并不是要求它达到高端线路的性能。

但这项服务**购买当天**就出现了首次连接失败与间歇性 TCP 建连卡顿。我希望客服针对初始异常给出更有针对性的调查或合理处置，而不只是反复援引套餐说明。

我也承认：**IPdog 首次测试失败不等于初始 IP 已遭封锁**，不能因此直接认定我必然符合免费换 IP 的政策例外。不过，客服没有向我展示针对这次初始连接失败的具体技术排查依据。

最终，针对仅 **4.50 加元**的当天订单，客服提出扣除 **1 加元**退款费用。即使政策中确有收费条款，**我仍认为这个比例对于本次情况缺乏善意与灵活性**。尤其在我要求全额退款及管理层复核后，最后收到的是准备关闭工单的回复，让我感到失望。

## 四、我的诉求与当前结果

我提出过两种解决方式：**免费更换一次 IP**，或者**全额退还 4.50 加元且免收 1 加元手续费**。

VMISS 拒绝免费更换 IP，并提出扣费退款方案。**截至本文发布前，我并未确认接受该退款方案，也未声称退款已经完成。**

我写下这段经历，是希望其他购买者在选择廉价 VPS 前仔细阅读线路说明、换 IP 政策和退款条款；如果在意自己的运营商线路质量，最好尽早从实际使用网络进行测试并留存证据。

## 五、证据与隐私

拟附上的材料包括：订单日期和金额凭证、最初 IPdog 失败记录（如有）、Mac 测试日志和部分抓包、经脱敏的客服工单截图。**若没有 IPdog 原始截图，就只保留“本人当时测试失败”的陈述，不应伪造图片或补造日志。**

发布前必须删除邮箱、客户号、订单号、订阅链接、UUID、API Token、证书私钥、SSH 凭据及不必要的真实 IP 地址。
