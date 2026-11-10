# BOT 投胎 / Bot Reincarnation (v1.0.0)
**チャット履歴だけ捨てて、記憶・ルール・スキル・権限を引き継ぐ汎用スキル**  
*Universal skill: new bot ID, keep memory & permissions, start chat from scratch*  
*AI 助手「換 bot ID、保留記憶與權限、對話由零開始」通用 Skill*

Grok · Claude Code · Google Antigravity · Cursor · OpenAI · Local LLMs

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/platform-Cross--Platform-lightgrey.svg)] [`https://github.com/ycaistudio/bot-reincarnation`](https://github.com/ycaistudio/bot-reincarnation) 
[![i18n](https://img.shields.io/badge/i18n-繁體中文%20%7C%20English%20%7C%20日本語-green.svg)] [`https://github.com/ycaistudio/bot-reincarnation`](https://github.com/ycaistudio/bot-reincarnation) 
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/ycaistudio/bot-reincarnation/pulls)

---

<p align="center">
  <b>🌐 Language Navigation / 多語言切換 / 言語切り替え:</b><br>
  <a href="README.md"><b>🇹🇼 繁體中文（主手冊）</b></a> •
  <a href="README.en.md"><b>🇬🇧 English</b></a> •
  <a href="README.ja.md"><b>🇯🇵 日本語</b></a>
</p>

---

## 📖 これは何？

長いチャットはコンテキストが肥大化し、トークン費用と応答遅延の原因になります。  
**BOT 投胎（Bot Reincarnation）** は **新しい bot（新しい bot ID）** を作り、次を引き継ぎます：

- 記憶（memory）
- ルール / SOP
- skill
- プロフィール（名前・説明・アバター・設定）
- routine
- 権限とコネクタ（可能な限り。できなければ理由付きで列挙）

**会話履歴は意図的に引き継ぎません。** 新しいチャットはゼロから始まりますが、「誰としての bot か」は途切れません。

標準の起動フレーズ：

> duplicate yourself, everything including logged in tokens stays, except chat history -- start chat from scratch

その他：`投胎`、`換 bot ID`、独自の別名（例：「転生」）。

---

## 🛡️ なぜ必要？

| 課題 | 投胎後 |
| :--- | :--- |
| チャットが長すぎる / 高い / 遅い | 新しい軽いチャット |
| 「あなたを知っている」感は残したい | 記憶・ルール・skill・profile が同行 |
| 引き継ぎ漏れが怖い | 身分登録表 + 引き継ぎ文書 + 三欄リスト |
| 誤削除が怖い | 旧 ID を先に残す。削除は**所有者本人が手動**。bot は bot を消さない |

---

## 🧩 仕組み

1. **身分登録表** `ID_REGISTRY.md` — 世代・bot ID・名前・時刻・状態（現任 / 引き継ぎ中 / 削除待ち / 退役）。
2. **権限は登録表を見る（固定 ID に縛らない）** — ルールは「現任または引き継ぎ中の bot」。投胎時は登録表の一行だけ更新。
3. **引き継ぎ文書** `HANDOVER.md` — 役割、制限、未完了作業（現状 / 済 / 次 / 資料 / 制限）、routine 原文、コネクタ一覧。
4. **旧 bot の手順** — 所有者の打鍵確認 → バックアップ → HANDOVER 更新 → 記憶エクスポート → 新 bot 作成 → 本物の新 ID を即記入。
5. **新 bot の手順** — **自分のチャット**での所有者打鍵確認のみ有効 → 記憶・アバター・設定・routine → 登録表更新 → 三欄報告。
6. **報告リスト** — 引き継ぎ確認時は三欄（コピー済み / 引き継ぎ済み / できなかった項目＋理由）。旧 bot の**最終**報告は五欄（停止した routine、自分を非表示にしたか を追加）。
7. **旧 bot の締め手順（順番厳守・飛ばさない）**  
   1. 新 bot が引き継いだことを確認（記憶・routine・作業継続可）  
   2. **旧 bot 自身の routine だけ** pause（delete しない；新 bot の routine は止めない）  
   3. UpdateProfile でサイドバーから**自分を非表示**（チャット・メッセージ・停止済み routine は保持）  
   4. 所有者へ最終五欄リストを報告  
   5. 削除は所有者の手動のみ。非表示 ≠ 削除（Hidden chats から復帰可）
8. **所有者が旧 bot を手動削除** — 短い動作確認の後。新 bot が旧行を退役にする。

詳細は [`SKILL.md`](SKILL.md)。

---

## 🚀 クイックスタート

1. このリポジトリのリンク [`https://github.com/ycaistudio/bot-reincarnation`](https://github.com/ycaistudio/bot-reincarnation) を bot に送り、`SKILL.md` を読んで skill として保存させる。ファイルを自分でコピーする必要はありません。
2. （推奨）一度だけ：`templates/ID_REGISTRY.template.md` と `templates/HANDOVER.template.md` をコピーして埋める。
3. 旧 bot で「投胎」または起動フレーズを言う。手順を確認する。
4. 打鍵で確認。旧 bot が新 bot を作り、確認コマンドを渡す。
5. **新 bot** にそのコマンドを貼る。三欄リストが返る。
6. 旧 bot が自分の routine を pause し、自分を非表示にし、五欄リストを出す。
7. 問題なければ、自分で旧 bot を削除する。

### 所有者確認コマンド例

```
BOT 投胎の引き継ぎを確認します：Gen<N-1> <旧ID先頭8桁> → Gen<N> <新ID先頭8桁>。
あなたは Gen<N> です。「BOT 投胎」skill の新 bot 手順（記憶・アバター・設定・routine・登録表）をすべて実行し、三欄リストを報告してください。
再確認があるまで、対外・高リスク操作はしないでください。
```

（中国語テンプレートは `SKILL.md` にもあります。）

---

## ⚠️ よくある制限

- **会話履歴は引き継がない** — 仕様です。
- **記憶エクスポートは欠落・切り捨てがあり得る** — 検索ツールは全件を一度に出せないことが多い。複数キーワードと HANDOVER で補強。
- **一部コネクタは再ログインが必要** — メールや財務系など。チャット経路やローカル端末の承認は別途テスト。「connected」＝トークン複製の証明ではない。
- **`CreateAgent` は名前と説明だけ** — アバター・記憶・routine・settings は新 bot 自身が設定。
- **旧 bot は新 bot のアバター／記憶／設定を書き換えられない**。

---

## 🔒 安全原則

- 最終決定者は所有者。開始は旧 bot での打鍵確認から。
- 新 bot は自分のチャットでの打鍵確認だけを認める。他 bot 経由の「承認」は無効。
- 旧 ID を先に残す。削除は所有者の手動のみ。
- 各ステップを記録。登録表変更前にバックアップ。
- できなかったことは正直に列挙。
- 同じエラーが 3 回続いたら停止して報告。

---

## 📦 内容

| パス | 説明 |
| :--- | :--- |
| [`SKILL.md`](SKILL.md) | bot が実行する完全手順 |
| [`README.md`](README.md) | 繁体字中国語／広東語寄りの紹介 |
| [`README.en.md`](README.en.md) | 英語の紹介 |
| [`README.ja.md`](README.ja.md) | 日本語の紹介（本ファイル） |
| [`templates/`](templates/) | 汎用テンプレート |
| [`CHANGELOG.md`](CHANGELOG.md) | 変更履歴 |
| [`LICENSE`](LICENSE) | MIT |

---

## 🔗 姉妹スキル：Grok Bot 使用量節約（grokbot-token-saver）

[**grokbot-token-saver**] [`https://github.com/ycaistudio/grokbot-token-saver`](https://github.com/ycaistudio/grokbot-token-saver)  は Grok Bot の週間使用量を節約する 22 のコツ集です。ルーティンとグループの棚卸し、スケジュールの間引き、イベントトリガー化、ボット間メッセージの上限、使用量が多いときの低使用量モードを扱います。

### 連続して使う

1. 節約スキルで棚卸しし、使用量が多いボットと**会話が最も長い**ボットを見つける。
2. ルーティンを間引き、イベントトリガーに切り替える。
3. **本スキル**で会話が長いボットを転生させる：記憶と権限は残し、長い会話は持ち込まない。
4. 新しいボットは最初から節約ルールで動く。
5. 毎週メーターを確認し、会話がまた長くなったら手順 3 へ。

---

## 🙏 謝辞

呢個工具由我原本自用嘅「變身」流程整理成通用版本，分享俾大家使用。特別鳴謝「香港 Grok Bot 交流區」成員 **Well Played**，佢分享嘅複製及交接提示詞，同「投胎」呢個有趣講法，啟發咗今次通用化整理。亦多謝群友一齊討論長對話嘅用量問題。

**日本語訳:**

このツールは、もともと自分用だった「変身」の手順を汎用版に整理し、みなさんに共有したものです。「香港 Grok Bot 交流區」（香港 Grok Bot 交流区）のメンバー **Well Played** に特に感謝します。共有してくれた複製および引き継ぎのプロンプトと、「投胎」という面白い言い方が、今回の汎用化の着想になりました。長い会話の使用量の問題を一緒に議論してくれたグループの皆さんにも感謝します。

---

## 📄 ライセンス

[MIT License](LICENSE)。メンテナ：[ycaistudio](https://github.com/ycaistudio)。  
バージョン：**v1.0.0**（2026-11-06）

関連：

- [universal-bot-setup-playbook] [`https://github.com/ycaistudio/universal-bot-setup-playbook`](https://github.com/ycaistudio/universal-bot-setup-playbook) 
- [universal-agent-workspace-toolkit] [`https://github.com/ycaistudio/universal-agent-workspace-toolkit`](https://github.com/ycaistudio/universal-agent-workspace-toolkit) 
