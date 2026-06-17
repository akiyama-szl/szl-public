# ムキムキクマ 共通 CTA カード

各話の最終コマとして使う固定 CTA 画像。**毎回 API 生成せず、ここに置いた `01.png` をコピーで使う運用**。

## ファイル

- `01.png` — 固定 CTA カード（1080×1350・PNG）
  - LINE 友達追加への導線
  - リンクマが手を振っているデザイン
  - 「個人店・中小企業のあなたへ」「登録、待ってるぜ！」「プロフィール欄のリンクから LINE で友達追加」

## 仕組み

`scripts/mukimuki_daily.py` の `append_static_cta()` が毎話の生成完了後に呼ばれ、`01.png` を最終コマの次の番号にコピーする：

```
ep-NN/01.png  ← 通常コマ（manga_generate_image.py が生成）
ep-NN/02.png
...
ep-NN/07.png  ← まとめ（ミニリンクマ・ホワイトボード）
ep-NN/08.png  ← 固定 CTA（このディレクトリの 01.png をコピー）
```

8 コマ拡張回（クール末話）の場合は `09.png` に CTA が入る。

## 更新方法

CTA デザインを変えたいときは、新しい `01.png`（1080×1350・PNG）でこのファイルを上書きしてコミットするだけ。次の話から自動的に新デザインが使われる。

過去話に遡って差し替える場合は、各 `published/manga/mukimuki-kuma/ep-NN/` の最後の番号 PNG を新しい `01.png` で上書きする。

## メリット

- ✅ API コストゼロ（毎話 1 枚分の生成費用を節約）
- ✅ デザインが完全に統一される（生成ごとのブレなし）
- ✅ 文字化け・レイアウト崩れのリスクなし
- ✅ 更新が即時反映される（次の話から）

## 関連

- 元の CTA 生成シナリオ（参考・履歴用）：`.claude/skills/manga-seisaku/scenarios/mukimuki-kuma/cta-line.json`
- 生成パイプライン：`scripts/mukimuki_daily.py` の `append_static_cta()`
- ワークフロー：`.github/workflows/mukimuki-daily.yml`
