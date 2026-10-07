# babuuu 秋・ハロウィン特集（引き継ぎメモ）

楽天ショップ「babuuu」（sid=422856）のキャンペーンページ一式。静的HTMLのみ（ビルド不要）。
公開: GitHub Pages `https://greentuushou-arch.github.io/babuuu-autumn-ouchi-feature/`（masterにpushで反映、数分かかる）

## ページ構成
| ファイル | 内容 |
|---|---|
| `index.html` | 秋のお出かけ×おうち時間LP（9〜10月前半用）。`game.html`をiframe埋め込み |
| `game.html` | まどそうじゲーム（窓の曇りをなぞる→クイズ→クーポン抽選）。クーポンURL設定済み |
| `index-halloween.html` | ハロウィンLP（オレンジ基調）。`game-halloween.html`をiframe埋め込み。**商品は仮カード（差し替え待ち）** |
| `game-halloween.html` | 「まほうのかがみ」（game.htmlの鏡版、ハロウィンPNG使用）。**COUPON_URLSが空欄** |
| `game-kigae.html` / `game-otoroi.html` / `game-gift.html` | 10月用に試作した別ゲーム案（きがえクイズ／神経衰弱／ギフトたたき）。未採用・参考 |
| `hellowin-*.png` | ハロウィンのクイズ用イラスト7種（kabocha, obake, koumori, neko, majo, candy, kumo） |
| `hellown-1.png` / `hellown-23.png` | クーポン結果の演出画像（1等／2・3等） |

## 未完了（次にやること）
1. `game-halloween.html` 上部の `COUPON_URLS`（first/second/third）に10月分の楽天クーポン取得URLを貼る。空欄の間は「クーポンを受け取る」ボタンは出ない。
2. `index-halloween.html` の仮商品（サンプル1〜5、「ここに見出しが はいります」）を実商品に差し替え。ハロウィン商品は無いため、見出しは「クーポンでおトクに買えるアイテム」の方針。
3. 商品カードは `index.html` のものが完成形（商品詳細ボタン・口コミボタン・タグ3つ・説明2文）。同じ構造で作る。価格・口コミ数は公開前に実ページで再確認する（過去に価格変更あり）。
4. 結果画面のクーポン額（1等100円/2等55円/3等39円）は `COUPON_TIERS` の `amount`。確率は `pickCouponOutcome()`（3%/60%/37%）。

## 重要な仕様・注意
- ゲーム→親ページ: iframe高さは `postMessage({type:'madoGameHeight'})` で自動調整。親側のリスナーを消さない。
- 「ゲームをしてみる」ボタンは `#game`（ゲーム枠）へ飛ばす。長いページでスムーズスクロールが止まるため、補正スクリプト（`behavior:'instant'`）が入っている。
- フォントは家具のソムリエ準拠: Noto Sans JP + Jost。字間 .03〜.05em・行間1.9以上で詰まらせない。
- スマホ表示（375px）を最優先。写真枠は `width:100%` を明示（SafariでaspectRatioだけだとはみ出すバグがあった）。
- ブラウザ/CDNキャッシュ: 同名ファイルを差し替えたらURLに `?v=2` を付けて確認・参照する。
- 商品データ取得: 商品ページの `og:image`、価格、売り切れは本文の「この商品は売り切れです」で判定。口コミURLは `https://review.rakuten.co.jp/item/1/422856_<内部コード>/1.1/`。
- 「傾いたピル型ラベル」「横スクロールUI」は使わない（ユーザー方針）。大きいタイトルに「、。」を付けない。

## ローカル確認
`python -m http.server 8942` をこのフォルダで起動し `http://localhost:8942/index-halloween.html` を開く（`file://`だとiframeが動かない）。
