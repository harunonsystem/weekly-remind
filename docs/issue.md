# Issue版の詳細設定

## ワークフローの設定

ファイル: `.github/workflows/weekly_report_issue.yml`

### スケジュール設定

```yaml
on:
  schedule:
    - cron: '0 13 * * 5'  # 毎週金曜22:00 JST（GitHub ActionsはUTCなのでJST-9）
```

### 必要な権限

```yaml
permissions:
  issues: write  # Issue作成権限
```

### 環境変数

- `ISSUE_LABEL`: Issue作成時に付与されるラベル（デフォルト: `weekly-report`）

## 動作の流れ

1. 指定したスケジュール時刻に、GitHub Actionsが起動
2. 新しいIssueを作成
   - タイトル: `[週報] YYYY/MM/DD`
   - 本文: 週報テンプレートと週報ページへのリンク
3. リポジトリオーナーにアサイン
4. 指定したラベルを付与
5. Issueを閉じることで週報完了を記録

## カスタマイズ

### ラベルの変更

`.github/workflows/weekly_report_issue.yml`の`env`セクションで設定できます：

```yaml
jobs:
  create_issue:
    env:
      ISSUE_LABEL: your-custom-label  # ラベル名を変更
```

### Issue本文のテンプレート変更

`.github/workflows/weekly_report_issue.yml`の`Create GitHub Issue`ステップで`--body`オプションを編集します：

```yaml
--body $'# 今週の週報\r\n\r\n- 記入したらこのIssueを閉じてください\r\n\r\n[週報ページへ](${{ secrets.WEEKLY_PAGE_URL }})'
``` 