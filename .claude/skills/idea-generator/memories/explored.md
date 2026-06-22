# Explored Domains — running memory across runs

The domain-picker reads this at the start of every run; the loop controller appends to it at the end of every run. Its job is to stop the picker from drifting back to the same few domains each run (memory resets between runs, so without this it re-discovers the same fee-shaving ideas).

## Classification rule (controller uses this when appending)

Classify each attempt by WHY it died — does the reason condemn the whole DOMAIN, or only this one IDEA?

- **GO** → an idea cleared the bar. Hard-avoid this domain forever (it's spent).
- **Dead domain** → killed for a reason that is structural to the DOMAIN: no real money moves here at all, a funded incumbent already owns the core, or a license/liability gates the whole space. Hard-avoid — a different idea won't fix it.
- **Explored, open** → killed for a reason specific to the IDEA, not the domain: this idea was a me-too, this idea needed maintained data, this idea's money thesis was weak — but a different angle in the same domain might still work. Soft-avoid (don't repeat the idea; only re-enter with a genuinely new angle).

## How the picker uses this

- **Hard-avoid**: never pick a domain listed under GO or Dead domain.
- **Soft-avoid**: avoid domains under Explored-open by default; only re-enter one if you have a genuinely different angle AND a different capture shape than the recorded miss.

---

## GO  (hard-avoid — won)

| date | domain | idea | captured money |
| --- | --- | --- | --- |
| 2026-06-20 | 確定申告の税理士前処理（記帳代行の肩代わり） | 丸投げパック | 記帳代行 年12〜36万を転用、申告のみ5〜7万 |
| 2026-06-20 | ユーザー車検の準備支援 | ジコシャケン | ディーラー車検6〜15万 → 法定費用約4.5万に圧縮 |
| 2026-06-20 | 古物商許可の自己申請（せどり/リユース開業） | コブツ申請ナビ | 行政書士代行 平均¥53,585 → 自己申請¥19,500、差¥3.4〜5万を圧縮 |
| 2026-06-21 | 建設業許可の自己申請（一人親方・小規模工務店） | 建設業許可ナビ | 行政書士費用15〜25万（知事許可新規） → 申請手数料9万のみ、差額15〜25万を圧縮 |
| 2026-06-21 | メンタルヘルス休職者の傷病手当金申請サポート | ショウビョウナビ | 社労士代行費¥30K〜¥100K/件 → 買い切り¥1,500で自己申請完結、差額ほぼ全額を圧縮 |
| 2026-06-22 | 宅地建物取引業（宅建業）免許の自己申請（宅建士合格者・副業不動産業開業者向け） | タッケンナビ | 行政書士代行費 10〜25万円（知事免許新規申請）→ 法定手数料¥33,000のみに圧縮 |

## Dead domains  (hard-avoid — structurally closed)

| date | domain | kill reason (domain-level) |
| --- | --- | --- |
| 2026-06-20 | 区分マンション兼業大家の運営 | incumbent占有：大家確定申告アプリが月120円で同一機能 |
| 2026-06-20 | 固定費（電気・通信）見直し | 比較サイト占有＋全プラン料金の構造的維持コスト |
| 2026-06-20 | 防災備蓄のローリングストック | 転用できる実在支払いが無い（回避コスト中心） |
| 2026-06-20 | オンライン英会話のサブスク疲れ | ELSA/Speak/Camblyが占有＋AI会話のAPI課金で買い切り不成立 |
| 2026-06-20 | 写真編集（Lightroom疲れ） | VSCO/Darkroom等の現像・フィルター系が占有 |
| 2026-06-20 | 食事記録（あすけん圏） | あすけんが10万メニューDB＋AI栄養士で占有、privacyは楔にならず |
| 2026-06-20 | 冠婚葬祭のご祝儀・お返し管理 | 記録のみ・回避コスト型で捕る金が無い |
| 2026-06-20 | 結婚式の最終見積もり最適化 | incumbent占有：中立の見積もり診断をウェディングニュース(無料LINE)/ハナユメ(無料人力)が広告主資金のlead-genで先行 |

## Explored, open  (soft-avoid — idea died, domain may survive a new angle)

| date | domain | dead idea | kill reason (idea-level) |
| --- | --- | --- | --- |
| 2026-06-20 | 社会人スポーツチームの幹事運営 | バンカン | 既存チーム運営アプリのme-too |
| 2026-06-20 | トレカのコレクション資産管理 | タナオロシ | この案が相場DBの常時維持を要する |
| 2026-06-20 | フリーランス翻訳者のワークフロー | （用語集＋単価可視化案） | 用語集はCATツールが占有・単価可視化はvitamin |
| 2026-06-21 | 相続登記の自己申請（不動産相続の法務局申請） | 相続登記ナビ | better相続登記（jp-better.com）がスマホ完結Webサービスとして¥8,250で先行占有 |
