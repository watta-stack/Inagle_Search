# Inagle_Search

# Inagle 検索（Inagle_Search）

Inagle の選手データを **拡張条件で検索**しつつ、よく出るビルドタイプを **「目印（タグ）」として付けて管理**できる、サーバ不要の静的ツールです。  
GitHub Pages に置けば **スマホでもURL開くだけ**で使えます。

## 公開URL（GitHub Pages）
- `https://watta-stack.github.io/Inagle_Search/`
- `https://watta-stack.github.io/Inagle_Search/index.html`

## 特徴
- **サーバ不要**：`index.html` + `out.data.js` + `build.tags.js` のみで動作
- **拡張検索**（例）
  - 名前 / シリーズ / ポジション / 属性 / 所属 / ステータスタイプ など
- **ビルドタイプ目印（6種）**での絞り込み
  - `正義 / 必殺 / ラフプレー / テンション / キズナ / カウンター`
  - 条件は **OR / AND** を切り替え可能
- 目印は **localStorage に保存**（ブラウザに残る）
- 必要なら、目印を **`build.tags.js` にエクスポート**して「手動管理ファイル」に統合できる

## ファイル構成
- `index.html`
  - UI/検索ロジック本体
  - localStorage キー：`INAGLE_BUILD_TAGS_V1`
- `out.data.js`
  - 選手データ（`window.OUT_DATA = [...]`）
- `build.tags.js`
  - 目印データ（`window.OUT_BUILD_TAGS = {...}`）
  - 手で編集して管理してもOK（エクスポートで更新も可能）

## 使い方（超ざっくり）
1. 公開URLを開く
2. 条件を入れて **「検索」**
3. 結果カードで目印（タグ）を付ける  
   → 目印は localStorage に保存されます

### 目印（タグ）の検索
- 「ビルドタイプ（目印から検索）」でタグを選択
- 条件は **OR / AND** を選べます
- 必要なら **「ビルド条件クリア」**で解除できます

### 目印を全部消す
- **「全選手の目印を全削除（localStorage）」**  
  ※ブラウザに保存している目印を消します（データファイルは消えません）

## build.tags.js へエクスポート
ページ内の **「build.tags.js をエクスポート」** を押すと、
- `build.tags.js`（既存の build.tags + localStorage の目印をマージしたもの）
をダウンロードできます。

> 使い方：ダウンロードした `build.tags.js` を、このリポジトリの `build.tags.js` に **手動で差し替え**てください。

## データ更新（out.data.js の差し替え）
1. 新しい `out.data.js` を用意（`window.OUT_DATA` 形式）
2. リポジトリの `out.data.js` を差し替え
3. commit & push  
→ GitHub Pages が更新されます

## Tips（スマホで更新が反映されないとき）
スマホのキャッシュで古いJSを掴むことがあります。  
強制再読み込みが効かない場合は、`index.html` の読み込みをこうすると安定します：

- `./out.data.js` → `./out.data.js?v=YYYYMMDD`
- `./build.tags.js` → `./build.tags.js?v=YYYYMMDD`

（例：`?v=20251229`）

## ライセンス / 注意
- 本ツールは静的サイトとして動作します（サーバ・DBなし）
- 目印（タグ）はブラウザの localStorage に保存されます
