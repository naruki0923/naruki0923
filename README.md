## naruki0923
毎日決まった時刻に外部サービスへ書き込むものを個人で運用していると、
落ちる・仕様が変わる・想定外の入力が来るのは前提になるので、
**失敗したときにどう振る舞うか**を先に決めてから作るようになりました。

Python でのバックエンド・自動化まわりが中心です。

---

### 🎬 SNS Content Automation Pipeline — [tiktok-pipeline](https://github.com/naruki0923/tiktok-pipeline)

SNS向けショート動画の
**リサーチ → 台本生成 → 音声生成 → 動画編集 → 投稿準備 → 分析**
までをほぼ自動化したシステムです。

- Python中心、約10,000行規模
- 約2か月以上継続運用
- 約100本の動画を生成
- 1本あたり約70分の作業を、最終確認・投稿操作のみの**約10秒**まで削減
- 最大10万回以上再生
- 運用開始後フォロワー約4,000人増加
- 毎週の投稿結果を分析し、リサーチ・台本生成プロンプトを改善
- エラー発生時はログ解析 → コード修正 → 再実行まで行う復旧フローを構築

特に、人が感覚的に行っていた「伸びる動画の選定基準」を言語化し、
AIが判断可能な形へ落とし込むことに力を入れました。

**Python / Playwright / VOICEVOX / Flask / discord.py / Cloudflare Workers**

---

### 🍚 AI Diet & Weight Management — [Weight-and-diet-management](https://github.com/naruki0923/Weight-and-diet-management)

食事管理を継続しやすくするため、
**写真を選ぶだけ**で食事内容・栄養情報を記録できる仕組みを開発しました。

- 食事写真からAIが内容・カロリー等を解析
- 商品パッケージの栄養表示も活用
- Apple Healthと体重計データを連携
- iOS Shortcutsを利用し、入力作業を最小化
- 約2か月継続運用

「入力を頑張る」のではなく、**入力そのものを減らすUX**を意識して設計しています。

**Python / FastAPI / Gemini API / Google Sheets API / Vercel**

---

### 🐱 Chappie — macOS常駐アシスタント — [chappie](https://github.com/naruki0923/chappie)

画面の隅に小さな猫が常駐し、「チャッピー、今日の予定」と声をかけるだけで
**予定確認・ファイル検索・一般の質問・Amazonの注文**まで行うネイティブアプリです。

- Swift / SwiftUI・AppKit で実装。メニューバー常駐、全デスクトップ表示、ログイン時起動
- 呼びかけ検出と文字起こしは Mac 内の音声認識で処理。カレンダー・Spotlight 検索も**ローカル完結**で AI に送らない
- 一般の質問は Codex CLI 経由で回答（read-only sandbox・一時セッションで実行）
- Amazon 購入は「商品・数量・送料込み上限・24時間の重複防止」をルールとして先に登録し、
  金額を読み上げて「いいよ」を得たあと**専用ブラウザで条件を再確認**してから注文
- ログイン・OTP・CAPTCHA・支払い方法の追加が必要な場面では**止まる**ように設計

「音声で何でもできる」より、**勝手に買わない・認証情報を扱わない**ための境界を先に決めて作りました。

**Swift / SwiftUI / AppKit / Speech / AVFoundation / EventKit / WebKit / Codex CLI**

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

`Python` `Swift` `asyncio` `FastAPI` `Flask` `SQLite` `Playwright` `Docker` `GitHub Actions` `Google Sheets API` `Gemini API` `Cloudflare (Tunnel / Workers)` `Vercel` `launchd`
