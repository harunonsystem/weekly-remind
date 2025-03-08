# Weekly Remind

毎週金曜日22:00（JST）に週報作成用のIssueを自動生成するGitHub Actions。

## 機能

- 毎週金曜日22:00（JST）に週報用Issueを自動作成
- 週報ページへのリンクをIssue内に自動追加
- リポジトリオーナーへの自動アサイン
- カスタマイズ可能なIssueラベル

## セットアップ

### 1. 必要なGitHub Secrets

以下の値をリポジトリのSecretsに設定してください：

- `WEEKLY_PAGE_URL`: 週報を書くページのURL（例: NotionのデータベースやConfluenceのページなど）

### 2. 必要なGitHubラベル

以下のラベルを作成してください：

- デフォルトでは`weekly-report`ラベルが使用されます
- 別のラベルを使用する場合は、`.github/workflows/weekly_report.yml`の`ISSUE_LABEL`環境変数を変更してください

### 3. GitHub Actionsの設定

デフォルトでは毎週金曜日22:00（JST）に実行されます。
スケジュールを変更する場合は、`.github/workflows/weekly_report.yml`の`cron`式を修正してください。

```yaml
on:
  schedule:
    - cron: '0 13 * * 5'  # 毎週金曜22:00 JST（GitHub ActionsはUTCなのでJST-9）
```

### 4. アサイン先について

Issueは自動的にリポジトリのオーナーにアサインされます。

## カスタマイズ

### ラベルの変更

`.github/workflows/weekly_report.yml`の`env`セクションで設定できます：

```yaml
jobs:
  create_issue:
    env:
      ISSUE_LABEL: your-custom-label  # ラベル名を変更
```

## 動作確認方法

1. GitHubリポジトリの"Actions"タブを開く
2. "Create Weekly Report Issue"ワークフローを選択
3. "Run workflow"をクリックして手動実行

## 注意事項

- GitHub Actionsの実行時間はUTCベースです（JST-9時間）
- Issueの自動生成にはGitHub Actionsの権限が必要です（デフォルトで設定済み） 