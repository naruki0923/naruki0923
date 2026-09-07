## naruki0923

個人で作ったシステムを、**作って終わりにせず動かし続けている**のが自分の中心にあります。
毎日決まった時刻に外部サービスへ書き込むものを個人で運用していると、
落ちる・仕様が変わる・想定外の入力が来るのは前提になるので、
**失敗したときにどう振る舞うか**を先に決めてから作るようになりました。

Python でのバックエンド・自動化まわりが中心です。

---

### 🎬 [tiktok-pipeline](https://github.com/naruki0923/tiktok-pipeline)

ショート動画の **リサーチ → 台本生成 → 動画生成 → 投稿 → 分析** を段ごとに切って自動化しています。
公開後の指標を回収して台本のルールに反映する、というループを回すのが目的です。

- **Python / Playwright / VOICEVOX / Flask / discord.py / Cloudflare Workers**
- 各段を独立したスクリプトにして、**途中の段から流し直せる**ようにしてある
- 進行は Discord bot から叩く。状態はダッシュボードで見る
- Python 61ファイル / 約10,600行

分析の段を後から足したのは、台本の重複判定が「この切り口は前に扱ったか」しか見ておらず、
**当たった切り口ほど「重複」で弾かれて二度と作れない**状態になっていたためです。
実績を持たせて「伸びた切り口は再訪してよい」と判定させるようにしました。

---

### 🍚 [Weight-and-diet-management](https://github.com/naruki0923/Weight-and-diet-management)

食事の写真から Gemini がカロリーと PFC を算出し、Google スプレッドシートに記録して、
その日の合計と「目標まであと何 kcal か」を返します。

- **Python / FastAPI / Gemini API / Google Sheets API / Vercel**
- 入力は **iOSショートカット**（写真を撮る → 共有 → タップ）。専用アプリを作らずに済ませた
- BMR / TDEE の計算はシートに依存しない純粋な関数に分けてある
- 設定の変更はスプレッドシートの「設定シート」を直接編集する（管理画面を作らない選択）

もともと LINE Bot でしたが、**入力に手数がかかって自分が続かなかった**ので、
写真を撮ってから記録が終わるまでのタップ数が最小になる形に作り直しました。

---

### 📈 [emaxis-discord-notifier](https://github.com/naruki0923/emaxis-discord-notifier)

投資信託の基準価額を公式サイトから取得して、毎朝8時に Discord へ通知します。
保有口数を設定すると評価額と損益も出ます。

- **Python / GitHub Actions（cron）/ Discord Webhook**
- 実行を GitHub Actions に置いたので、**Macの電源やスリープに影響されない**
- 土日祝も動かして「その時点で公表済みの直近営業日の値」を送る
- 保有情報はリポジトリに入れず Secrets に置く。更新用のスクリプトを別に用意

小さいものですが、**取得 → 整形 → 通知** を定期実行で回すのに必要なものが一通り入っています。

### 使っているもの

`Python` `asyncio` `FastAPI` `Flask` `SQLite` `Playwright` `Docker` `GitHub Actions` `Google Sheets API` `Gemini API` `Cloudflare (Tunnel / Workers)` `Vercel` `launchd`
