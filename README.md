# kenpo-daily-login

DK健保組合ポータル（dk.kenpo.gr.jp）に自動ログインする GitHub Actions ワークフローです。

**毎月10回ログインすると100ポイント**がもらえる特典があるため、それを自動で達成することが目的です。毎日実行することで月10回の条件を確実にクリアします。

## セットアップ

### 1. リポジトリをフォーク

右上の **Fork** ボタンからご自身のアカウントにフォークしてください。

### 2. Secrets を登録

フォーク先リポジトリの **Settings → Secrets and variables → Actions → New repository secret** から以下の3つを登録します。

| Secret 名 | 内容 |
|-----------|------|
| `KENPO_NO` | ログイン画面の「NO」欄 |
| `KENPO_ID` | ログイン画面の「ID」欄 |
| `KENPO_PWD` | パスワード |

### 3. Actions を有効化

フォーク直後は Actions が無効になっています。  
**Actions タブ → 「I understand my workflows, go ahead and enable them」** をクリックしてください。

以上で完了です。翌日 10:00 JST から自動実行されます。

## 動作確認

手動でテスト実行できます。

**Actions タブ → Daily Kenpo Login → Run workflow → Run workflow**

実行ログで `Login succeeded.` と表示されれば成功です。

## スケジュール

毎日 **10:00 JST**（UTC 01:00）に自動実行されます。

変更したい場合は `.github/workflows/daily-kenpo-login.yml` の `cron` を編集してください。

```yaml
- cron: '0 1 * * *'  # 01:00 UTC = 10:00 JST
```

[crontab.guru](https://crontab.guru/) で時刻を確認できます。

## 失敗時の通知

ログインに失敗すると GitHub からメール通知が届きます（GitHub アカウントの通知設定に依存）。  
Actions タブでエラー内容を確認してください。
