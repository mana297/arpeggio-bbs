# CHANGELOG

ARPEGGIO の変更履歴。バージョン完了時に必ず更新する。  
バグの詳細は [BUGLOG.md](BUGLOG.md) を、機能詳細は [FEATURELOG.md](FEATURELOG.md) を参照。

フォーマット: Added（新機能）/ Changed（変更）/ Fixed（バグ修正）/ Architecture（設計改善）

---

## [v1.1.1] 2026-05-24 — ステータスタグ

### Added
- ステータスタグ機能（FEAT-011）
  - 💬話せる / 👻幽霊 / 😴睡眠中 / 🏃外出中 / 💼仕事中 / 📚勉強中 / 🎮ゲーム中 / 🎵音楽中 / 🍜ご飯中 / 🛁お風呂中 / 😊気分いい / 😔憂鬱 / 😡イライラ / 🤔考え中 / 🌙まったり の16種
  - ヘッダー `STATUS` ボタン → モーダルで選択
  - メンバーリストに選択中の絵文字をリアルタイム表示
  - 再接続後もステータス維持

---

## [v1.0.1] 2026-05-24 — 開発体制整備

### Architecture
- DEV_WORKFLOW.md をベースに開発体制を確立
- README.md / CHANGELOG.md / BUGLOG.md / FEATURELOG.md を新規作成（FEAT-010）
- .gitignore を追加

---

## [v1.0.0] 2026-03-20 — 基盤完成

> v0.1〜v0.7 の開発期間を経て確定したベースライン。

### Added
- リアルタイムチャット（Firebase Realtime Database）（FEAT-001）
- パスワード認証（ユーザー / 管理者 2段階）（FEAT-001 / FEAT-004）
- アバターシステム（イニシャル＋カラーハッシュ）（FEAT-002）
- Twitter風掲示板（いいね・リプライ付き）（FEAT-008）
- オンラインメンバーリスト（リアルタイムプレゼンス）（FEAT-003）
- 管理者パネル（OBSERVER MODE・MUTE・削除・統計）（FEAT-004 / FEAT-006）
- スパム対策（3秒クールダウン）（FEAT-004）
- スラッシュコマンド（/help /members /me /clear /coin /8ball）（FEAT-006）
- 日付セパレーター・入退室通知（FEAT-005）
- Firebase 匿名認証（FEAT-009）

### Fixed
- BUG-001: ボード表示・通知・日付セパレーター不具合
- BUG-002: iOS 全角スラッシュ問題
- BUG-003: プレゼンス再接続失敗

---

## ロードマップ

```
v1.1  DM機能・ステータスタグ・リアクション絵文字
v1.2  写真投稿・Firebase Storage
v1.3  アカウント登録・友だちシステム（Bondee基盤）
v2.0  アバター・スペース・航海（Bondee MVP）
```
