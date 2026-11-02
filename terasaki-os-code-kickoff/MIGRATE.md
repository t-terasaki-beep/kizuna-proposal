# terasaki-os-code への移植手順

`terasaki-os-code` はこのセッションのスコープ外（GitHub権限は kizuna-proposal のみ）のため、
ここから直接プッシュはできません。代わりに、**1ファイルで全部を再現する自己完結インストーラ**
`setup_terasaki_os_code.sh` を用意しました。これを本物のリポジトリで実行すれば、パッケージ一式が
バイト単位で同一に展開されます（検証済み）。

## 方法A: 新セッション（terasaki-os-code）で展開 ★おすすめ

1. **claude.ai/code** で「新しいセッション」を作成し、リポジトリに **`t-terasaki-beep/terasaki-os-code`** を選ぶ。
2. お渡しした `setup_terasaki_os_code.sh` をそのセッションにアップロードする
   （チャットにファイル添付）。
3. 次のように頼む：

   > アップロードした setup_terasaki_os_code.sh をリポジトリのルートで実行して、
   > 展開された terasaki-os-code 一式をコミットし、プッシュしてください。
   > 展開後に `python3 engine/build_proposal.py customers/kizuna-home/inputs.json` を実行し、
   > 生成された index.html が壊れていないか確認してください。

   セッションが `bash setup_terasaki_os_code.sh` を実行 → 全ファイルが出現 → コミット&プッシュします。

## 方法B: ローカルPCで展開して自分でプッシュ

```bash
git clone https://github.com/t-terasaki-beep/terasaki-os-code.git
cd terasaki-os-code
bash /path/to/setup_terasaki_os_code.sh      # 一式を展開
python3 engine/build_proposal.py customers/kizuna-home/inputs.json   # 動作確認
git add .
git commit -m "Initialize terasaki-os-code proposal engine"
git push origin main      # または任意のブランチ
```

## 展開されるもの

```
CLAUDE.md                         # OSの頭脳（寺嵜流の定義）
README.md                         # 使い方
.gitignore
data/inputs.schema.json           # 入力スキーマ
engine/diagnose.py                # 数値診断
engine/build_proposal.py          # スライド+ナレーション生成
engine/mp3gen.py                  # MP3生成
templates/shell.html              # デザイン共通シェル
knowledge/methodology.md          # 計算式と論法の根拠
customers/kizuna-home/inputs.json # 再現用サンプル
```

`index.html` / `narration.txt` / `audio/` は生成物なので含めていません
（`build_proposal.py` / `mp3gen.py` でいつでも再生成できます）。

## 動作確認の合格ライン

`python3 engine/diagnose.py customers/kizuna-home/inputs.json` の出力が、元のKIZUNA提案と一致すること：

- Aプラン: 自己負担 1,671万 / 回収 6.0年 → 満床4.1年
- Bプラン: 自己負担 2,448万 / 回収 7.6年 → 満床4.4年 / 20年累計 **8,712万**
