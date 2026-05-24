# ARPEGGIO 実装ログ

全機能の実装記録。新機能・アーキテクチャ改善を追加したタイミングで必ずここに追記する。

---

## 記録フォーマット

```
### FEAT-XXX: 機能概要
- **実装バージョン**: vX.Y
- **実装日**: YYYY-MM-DD
- **種別**: 新機能 / アーキテクチャ / UI / バグ修正
- **実装内容**: 何を・どこに・どう実装したか
- **関連コード**: 関数名・変数名・セクション名
```

---

## v0.x — 初期開発期（DEV_WORKFLOW 導入前）

### FEAT-001: 初期実装（チャットUI・パスワード認証）
- **実装バージョン**: v0.1
- **実装日**: 2026-03-xx（git: `Initial commit`）
- **種別**: 新機能
- **実装内容**: HTML単一ファイル構成でパスワード入力画面・リアルタイムチャットを実装。Firebase Realtime Database と接続。Share Tech Mono / VT323 フォントによるレトロターミナルUI。スパムは未対策。
- **関連コード**: `#pw`（パスワード画面）、`#chat`（チャット）、`addChat()`、`sendChat()`

### FEAT-002: アバター・ボードタブ追加
- **実装バージョン**: v0.2
- **実装日**: 2026-03-xx（git: `feat: avatar + board tab`）
- **種別**: 新機能
- **実装内容**: ユーザーのイニシャルから色を生成するアバターシステム（`avClass()` / `avText()`）。CHAT / BOARD の2タブ構成を導入。ボードの初期実装（投稿フォームのみ）。
- **関連コード**: `avClass()`、`avText()`、`mkAv()`、`.tabs`、`#bbs`

### FEAT-003: オンラインメンバーリスト（プレゼンス）
- **実装バージョン**: v0.3
- **実装日**: 2026-03-xx（git: `feat: online member list`）
- **種別**: 新機能
- **実装内容**: Firebase Realtime DB の `presence/` ノードでオンラインユーザーをリアルタイム管理。onDisconnect でタブを閉じたときに自動削除。メンバーパネル（サイドバー）に一覧表示。オンライン数をヘッダーに表示。
- **関連コード**: `updateMembers()`、`presence/`（DBノード）、`.members-panel`

### FEAT-004: 管理者モード・スパム対策
- **実装バージョン**: v0.4
- **実装日**: 2026-03-xx（git: `feat: admin mode + spam protection`）
- **種別**: 新機能
- **実装内容**: パスワード2段階（ユーザー: `arpeggio` / 管理者: `izaya`）。管理者は MUTE・DEL 操作が可能。3秒クールダウンによるスパム防止（`SPAM_MS=3000`）。MUTE したユーザーのメッセージを半透明表示。
- **関連コード**: `isAdmin`、`mutedUsers`、`SPAM_MS`、`addSpamWarn()`

### FEAT-005: ボードバグ修正・入室通知・日付セパレーター・名前保存
- **実装バージョン**: v0.4.1
- **実装日**: 2026-03-xx（git: `fix: board bug, notices, date sep, name save`）
- **種別**: バグ修正 / UI
- **実装内容**: ボード表示バグ修正。入退室通知（`addNotice()`）。日付をまたいだときのセパレーター表示（`dateLabel()` / `lastDL`）。ニックネームの localStorage 保存（`SAVED_KEY`）と前回名前のヒント表示。
- **関連コード**: `addNotice()`、`dateLabel()`、`lastDL`、`SAVED_KEY`

### FEAT-006: 管理者パネル・掲示板修正・スラッシュコマンド
- **実装バージョン**: v0.5
- **実装日**: 2026-03-xx（git: `feat: admin panel, board fix, slash commands`）
- **種別**: 新機能
- **実装内容**: 管理者用フローティングパネル（OBSERVER MODE）。統計表示（オンライン数・メッセージ数・投稿数・MUTE数）。スラッシュコマンド実装（`/help` `/members` `/me` `/clear` `/coin` `/8ball`）。掲示板の追加修正。
- **関連コード**: `handleCmd()`、`.admin-fab`、`.admin-panel`、`updateAdminStats()`

### FEAT-007: iOS スラッシュ正規化・プレゼンス再接続
- **実装バージョン**: v0.5.1
- **実装日**: 2026-03-xx（git: `fix: iOS slash commands, presence reconnect`）
- **種別**: バグ修正
- **実装内容**: iOS キーボードの全角スラッシュ（／）を半角に正規化（`normalizeSlash()`）。Firebase 切断後のプレゼンス再接続対応（`.info/connected` で再設定）。
- **関連コード**: `normalizeSlash()`、`onValue(ref(db, '.info/connected'), ...)`

### FEAT-008: Twitter風ボード（いいね・リプライ）
- **実装バージョン**: v0.6
- **実装日**: 2026-03-xx（git: `feat: twitter-like board with likes and replies`）
- **種別**: 新機能
- **実装内容**: 掲示板をTwitter風にリニューアル。投稿カード（`buildPostCard()`）、いいね機能（`postLikes/` ノード・localStorage 管理）、リプライ機能（`postReplies/` ノード）。投稿は `posts2/` ノードで新規管理。全件再描画方式（`redrawBoard()`）。
- **関連コード**: `buildPostCard()`、`redrawBoard()`、`likedPosts`、`posts2/`、`postLikes/`、`postReplies/`

### FEAT-009: Firebase 匿名認証
- **実装バージョン**: v0.7 → **v1.0 として確定**
- **実装日**: 2026-03-xx（git: `feat: firebase anonymous auth`）
- **種別**: アーキテクチャ
- **実装内容**: Firebase Anonymous Auth を導入。パスワード認証後に `signInAnonymously()` を呼び出し、Firebase Security Rules を有効化できる基盤を整備。接続中はボタンを `CONNECTING...` 表示に変更。
- **関連コード**: `signInAnonymously()`、`enter()`、`startChat()`

---

## v1.0 — 基盤完成（DEV_WORKFLOW 導入・ドキュメント整備）

### FEAT-010: 開発ドキュメント整備・DEV_WORKFLOW 導入
- **実装バージョン**: v1.0.1
- **実装日**: 2026-05-24
- **種別**: アーキテクチャ
- **実装内容**: DEV_WORKFLOW.md をベースに開発体制を確立。README.md / CHANGELOG.md / BUGLOG.md / FEATURELOG.md を新規作成。.gitignore を追加。git 履歴を遡って FEAT-001〜009 を記録。
- **関連コード**: 各 .md ファイル、.gitignore
