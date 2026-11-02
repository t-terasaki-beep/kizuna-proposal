# 引き継ぎ資料 — KIZUNA HOME提案 ＆ terasaki-os-code（提案自動生成OS）

最終更新: 2026-11（GitHub/Notion 再接続後に復元）
対象リポジトリ: `t-terasaki-beep/kizuna-proposal`（**公開リポジトリ**）
作業ブランチ: `claude/terasaki-os-code-setup-ljhwqt` / PR: **#3**

> ⚠️ このリポジトリは公開です。お客様の個人メール・携帯番号などの**個人情報は本資料に記載しません**。
> 宛先等は Gmail の該当スレッド／下書き、または Notion「寺嵜OS」を参照してください。

---

## 1. 全体のゴール（オーナーの意図）

- **terasaki-os-code** を「寺嵜流 提案自動生成OS」として育て、寺嵜の代わりに省エネ・脱炭素の営業提案を量産する。
- 最終目標は「毎月500万円の利益」。
- 正直な位置づけ: OSは利益を直接生まない。**提案の質と本数を底上げ**し、商談数 × 決定率 = 月次利益のレバーを上げるのが役割。

## 2. 現在地（サマリ）

| 項目 | 状態 |
|---|---|
| 提案自動生成エンジン（terasaki-os-code/） | ✅ 実装済み・KIZUNA実績で検算一致・**リモート反映済み** |
| 別リポ terasaki-os-code への移植キット | ✅ `terasaki-os-code-kickoff/`（自己完結インストーラ含む）反映済み |
| KIZUNA提案HTML（標準・ミニマム） | ✅ GitHub Pagesで公開中 |
| Netlifyへの移行 | ⏳ 配布zip作成済み（オーナー手元）・**手動デプロイ待ち** |
| お客様フォローメール | ✅ Gmail下書き作成済み・**送信待ち**（送信は人手） |
| PR #3 | ⏳ オープン（レビュー/マージ待ち。CI無し・コメント無し） |
| Notion「寺嵜OS」連携 | ✅ 接続確認済み（司令塔・案件ページあり） |

## 3. 成果物と場所

### 3-1. 提案自動生成OS本体 — `terasaki-os-code/`（リモート反映済み）
```
terasaki-os-code/
  CLAUDE.md                         # OSの頭脳（寺嵜流の型・口調・運用ルール）
  README.md                         # 使い方
  data/inputs.schema.json           # 入力スキーマ
  engine/diagnose.py                # 数値診断（自己負担・回収年数・20年累計）
  engine/build_proposal.py          # 入力→8枚スライド+ナレーション→index.html
  engine/mp3gen.py                  # ナレーション→MP3(edge-tts ja-JP-NanamiNeural)
  templates/shell.html              # デザイン共通シェル（KIZUNAのCSS/JS継承）
  knowledge/methodology.md          # 計算式と論法の根拠
  customers/kizuna-home/inputs.json # 再現サンプル
```
使い方:
```
python3 engine/diagnose.py        customers/kizuna-home/inputs.json
python3 engine/build_proposal.py  customers/kizuna-home/inputs.json
python3 engine/mp3gen.py          customers/kizuna-home/inputs.json   # 要 pip install edge-tts
```

### 3-2. 別リポ terasaki-os-code への移植キット — `terasaki-os-code-kickoff/`
- `setup_terasaki_os_code.sh` … 1ファイルで全部を再現する自己完結インストーラ（検証済み）
- `MIGRATE.md` / `KICKOFF_PROMPT.md` / `CLAUDE.md`

### 3-3. KIZUNA提案HTML（公開中）
- 標準（太陽光78.75kW／A・B 2プラン）: ルート `index.html`
- ミニマム再提案（太陽光最小57.5kW）: `min/index.html`
- ナレーションはブラウザ音声(TTS)が主、MP3が予備。

## 4. 公開リンク
- GitHub Pages 標準: https://t-terasaki-beep.github.io/kizuna-proposal/
- GitHub Pages ミニマム: https://t-terasaki-beep.github.io/kizuna-proposal/min/
- Netlify（移行先・手動デプロイ待ち）: `kizuna-netlify.zip` を https://app.netlify.com/drop にD&D → 発行URLで下書きのリンクを差し替え。

## 5. お客様フォローメール（Gmail下書き・送信待ち）
- 状態: **下書き作成済み（未送信）**。宛先/CC/本文詳細は Gmail下書き本体を参照（個人情報のため非記載）。
- 形式: 6/11「要点版」提案メールへの返信。
- 骨子: 「その後いかがでしょうか／再度ご案内」＋「補助金と構成調整で蓄電池込み約6年少々で回収（本来15年のところを調整）」＋標準/ミニマム2リンク＋「ご判断はお客様のペースで」＋寺嵜署名。
- 次アクション: ①Netlify URLに差し替え → ②オーナーが送信。

## 6. KIZUNA案件の主要数値（提案書より・検算済み）

| | Aプラン(補助金最適化) | Bプラン(削減最大化) |
|---|---|---|
| 投資総額 | 2,167万 | 2,944万 |
| 補助金 | ▲496万 | ▲496万 |
| 自己負担 | 1,671万 | 2,448万 |
| 回収(現状→満床) | 6.0→4.1年 | 7.6→4.4年 |
| 年間削減(現状/満床) | 277/408万 | 322/558万 |
| 20年累計 | 6,489万 | **8,712万** |

- 設備: 太陽光78.75kW / 蓄電池40.5kWh(Powerwall3×3) / 窓コーティング。ミニマム版は太陽光57.5kW。
- 省エネ診断: レナリア(担当 大杉様)が6/3実施。
- 補助金: 千葉県脱炭素化促進事業／ストレージパリティ等。**交付決定前の契約・着工は対象外**。

## 7. 既知の問題・制約（履歴）
1. 一時期 git push / 外部URL が 403（環境の通信制限）。**コンテナ再初期化で未プッシュだった handover と root .gitignore は消失**（handoverは本ファイルで復元）。以降は GitHub MCP 経由での push が安定。
2. Netlify / Gmail送信はツール無し → デプロイ・送信は人手。
3. MP3とaudio/の参照不一致（デッキは `audio/NN.mp3` 参照、ルートmp3は 01〜07）。TTSが全スライドを賄うため実害小。Netlify用zipでは `audio/` に配置済み。
4. terasaki-os-code 本リポはこのセッションのスコープ外 → 移植キットで対応。

## 8. 次のアクション（優先順）
1. Netlifyに公開 → 発行URLを控える。
2. Gmail下書きのリンクをNetlify URLに差し替え → 送信。
3. （任意）PR #3 をレビュー/マージ。
4. terasaki-os-code 本リポへ移植（`setup_terasaki_os_code.sh` を新セッションで実行）。
5. 2件目の顧客で実戦投入（`customers/<新顧客>/inputs.json`）。
6. 成約/失注を `knowledge/` に蓄積し、OSを継続的に賢く。

## 9. 環境メモ
- GitHubスコープは `t-terasaki-beep/kizuna-proposal` のみ。別リポは新セッションで選択。
- 操作アカウント(Gmail/Notion等): `live.in.japan0219@gmail.com`。提案メール送信元は会社アドレス。
- Notion「🧭 寺嵜OS — 営業司令塔」に案件・顧客・補助金・商材を集約。
