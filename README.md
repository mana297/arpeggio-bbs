# ARPEGGIO

> 匿名コミュニティ Web アプリ。パスワードを知っている人だけが入れる、クローズドな場所。

---

## コンセプト

デュラララのダラーズにインスパイアされた、匿名チャット＆掲示板コミュニティ。  
匿名 Twitter / 2ちゃんねるの代替を目指しつつ、Bondee 的なアバター・ステータス共有・近距離SNS体験も取り込んでいく。

---

## 技術スタック

| 項目 | 内容 |
|------|------|
| フロントエンド | HTML / CSS / Vanilla JS（単一ファイル構成） |
| バックエンド | Firebase Realtime Database |
| 認証 | Firebase Anonymous Auth |
| ホスティング | GitHub Pages（予定） |
| フォント | Share Tech Mono / VT323 |

---

## 現在の機能

- パスワード認証（ユーザー / 管理者の2段階）
- リアルタイムチャット（Firebase）
- 掲示板（Twitter風・いいね・リプライ付き）
- オンラインメンバーリスト（プレゼンス管理）
- 管理者パネル（OBSERVER MODE）：削除・MUTE・統計
- スパム対策（3秒クールダウン）
- スラッシュコマンド（`/help` `/members` `/me` `/clear` `/coin` `/8ball`）
- 日付セパレーター
- モバイル対応（iOS スラッシュ正規化）

---

## セキュリティメモ

- Firebase API キーは公開鍵のため、コミットに含まれていても問題なし（セキュリティはFirebaseセキュリティルールで制御）
- パスワード（USER_PW / ADMIN_PW）は `index.html` 内にハードコード。趣味プロジェクトとして許容しているが、将来的には Firebase Remote Config 等への移行を検討

---

## 開発ドキュメント

| ファイル | 内容 |
|---------|------|
| [CHANGELOG.md](CHANGELOG.md) | バージョン別の変更概要 |
| [FEATURELOG.md](FEATURELOG.md) | 全機能の実装記録 |
| [BUGLOG.md](BUGLOG.md) | バグ・エンバグの記録 |
| [DEV_WORKFLOW.md](DEV_WORKFLOW.md) | 開発体制・フロー |

---

## ロードマップ

```
v1.0  現在（基盤完成）
v1.1  DM機能・ステータスタグ・リアクション絵文字
v1.2  写真投稿・Firebase Storage
v1.3  アカウント登録・友だちシステム（Bondee基盤）
v2.0  アバター・スペース・航海（Bondee MVP）
```
