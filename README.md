# Weekly Remind

毎週金曜日22:00（JST）に週報記録用のIssue/Pull Requestを自動生成するGitHub Actions。
Issue作成とPull Request作成の2つのワークフローが用意されており、用途に応じて選択できます。

## 機能

共通機能:
- 毎週金曜日22:00（JST）に週報記録の自動作成
- 週報ページへのリンクを自動追加
- カスタマイズ可能なラベル

Issue版:
- GitHubのIssueとして週報を管理
- リポジトリオーナーへの自動アサイン
- [詳細設定](docs/issue.md)

Pull Request版:
- `RECORD.md`に完了済みの日付を自動追加
- GitHubのPull Requestとして記録を管理
- マージによる記録の履歴管理
- シンプルな記録形式（`[x] YYYY/MM/DD`）
- [詳細設定](docs/pull-request.md)

## 基本セットアップ

1. リポジトリのSecretsに`WEEKLY_PAGE_URL`を設定
2. `weekly-report`ラベルを作成
3. 使用したいワークフローのコメントアウトを解除
   - Issue版: `.github/workflows/weekly_report_issue.yml`
   - PR版: `.github/workflows/weekly_report_pr.yml`

## 動作確認方法

1. GitHubリポジトリの"Actions"タブを開く
2. 使用したいワークフローを選択
3. "Run workflow"をクリックして手動実行

## 注意事項

- GitHub Actionsの実行時間はUTCベースです（JST-9時間）
- Issue版とPull Request版は同時に有効にすることも可能ですが、通常は片方のみを使用することを推奨します 