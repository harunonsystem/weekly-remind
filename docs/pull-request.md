# Pull Request版の詳細設定

## ワークフローの設定

ファイル: `.github/workflows/weekly_report_pr.yml`

### スケジュール設定

```yaml
on:
  schedule:
    - cron: '0 13 * * 5'  # 毎週金曜22:00 JST（GitHub ActionsはUTCなのでJST-9）
```

### 必要な権限
Repository Settnigs > Actions > General から Workflow permissons `Read and write permissions
`に設定してください。
```yaml
permissions:
  contents: write      # リポジトリへのpush権限
  pull-requests: write # PR作成権限
```

### 環境変数

- `BRANCH_NAME`: 作成されるブランチのベース名（デフォルト: `weekly-report`）

## 動作の流れ

1. 指定したスケジュール時刻に、GitHub Actionsが起動
2. リポジトリをチェックアウト
3. 新しいブランチを作成（`weekly-report/YYYYMMDD`形式）
4. `RECORD.md`に新しい日付を追加
   - 形式: `[x] YYYY/MM/DD`（週報完了としてマーク）
5. 変更をコミット
6. Pull Requestを作成
   - タイトル: `週報: YYYY/MM/DD`
   - 本文: 週報テンプレートと週報ページへのリンク
7. PRをマージすることで、週報の記録が更新

## カスタマイズ

### ブランチ名の変更

`.github/workflows/weekly_report_pr.yml`の`env`セクションで設定できます：

```yaml
jobs:
  create_pr:
    env:
      BRANCH_NAME: your-custom-branch-name  # ブランチ名のベースを変更
```

### Pull Request本文のテンプレート変更

`.github/workflows/weekly_report_pr.yml`の`Create Pull Request`ステップで`--body`オプションを編集します：

```yaml
--body "# 今週の週報記録\n\n週報の記録を追加します。\n\n[週報ページへ](${{ secrets.WEEKLY_PAGE_URL }})"
```

### RECORD.mdの記録形式

`.github/workflows/weekly_report_pr.yml`の`Update RECORD.md`ステップで編集します：

```yaml
echo "[x] ${{ env.DATE }}" >> RECORD.md  # 週報完了としてマーク
```

記録は最初から完了状態（`[x]`）としてマークされます。これにより：
- 週報の記録がシンプルに
- マージ後の追加の更新が不要
- 履歴が明確に管理可能 