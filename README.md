# kenpo-daily-login

DK健保組合ポータル（dk.kenpo.gr.jp）に自動ログインする GitHub Actions ワークフローです。

**毎月10回ログインすると100ポイント**がもらえる特典があるため、それを自動で達成することが目的です。毎日実行することで月10回の条件を確実にクリアします。

ログイン後に「今月n回目」のログイン回数を読み取り、Discord に通知します。

## セットアップ

### 1. リポジトリをフォーク

右上の **Fork** ボタンからご自身のアカウントにフォークしてください。

### 2. Secrets を登録

フォーク先リポジトリの **Settings → Secrets and variables → Actions → New repository secret** から以下を登録します。

| Secret 名 | 内容 |
|-----------|------|
| `KENPO_NO` | ログイン画面の「NO」欄 |
| `KENPO_ID` | ログイン画面の「ID」欄 |
| `KENPO_PWD` | パスワード |
| `DISCORD_WEBHOOK_URL` | Discord の Webhook URL |

Discord Webhook URL の取得方法: チャンネル設定 → 連携サービス → ウェブフック → 新しいウェブフック

### 3. Actions を有効化

フォーク直後は Actions が無効になっています。  
**Actions タブ → 「I understand my workflows, go ahead and enable them」** をクリックしてください。

以上で完了です。翌日 8:45 JST から自動実行されます。

## Discord 通知

ログインのたびに Discord へ通知が届きます。

- **成功時:** 今月何回目のログインかを表示
- **失敗時:** Actions ログへのリンク付きでエラーを通知

## 動作確認

手動でテスト実行できます。

**Actions タブ → Daily Kenpo Login → Run workflow → Run workflow**

実行ログで `Login succeeded.` と表示され、Discord に通知が届けば成功です。

## スケジュール

**2日に1回** 8:45 JST（UTC 23:45）に自動実行されます。月約15回実行されるので、10回の条件を余裕でクリアします。

変更したい場合は `.github/workflows/daily-kenpo-login.yml` の `cron` を編集してください。

```yaml
- cron: '45 23 */2 * *'  # 23:45 UTC = 08:45 JST（2日に1回）
```

[crontab.guru](https://crontab.guru/) で時刻を確認できます。
