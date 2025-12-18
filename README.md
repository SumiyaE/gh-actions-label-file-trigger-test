# GitHub Actions: Label + File Trigger Test

GitHub Actions で **ラベル条件** と **ファイルトリガー（paths）** を組み合わせた場合の動作を検証するリポジトリです。

## ワークフローの条件

- **トリガー**: `pull_request` イベント（labeled, synchronize, opened, reopened）
- **paths**: `file1-a`, `file2-a` のみ
- **ラベル条件**: `test:gauge` ラベルが付与されている場合のみ実行

## ファイル構成

| ファイル | ワークフロートリガー対象 |
|---------|----------------------|
| `file1-a` | ✅ Yes |
| `file2-a` | ✅ Yes |
| `file1-b` | ❌ No |

## 検証項目

- [ ] ラベル `test:gauge` を付与してワークフローが動くことを確認
- [ ] ラベルを外した後、`file1-a` または `file2-a` を変更してpushし、ワークフローが**動かない**ことを確認
- [ ] ラベル `test:gauge` を再度付与した後、コミットしてpushし、ワークフローが動くことを確認

## 検証手順

1. `main` からブランチを切る
2. `file1-a` を変更してPRを作成
3. PRに `test:gauge` ラベルを付与 → ワークフロー実行を確認
4. ラベルを外す
5. `file1-a` を再度変更してpush → ワークフローが実行されないことを確認
6. ラベルを再度付与 → ワークフローが実行されることを確認（labeledイベント）
