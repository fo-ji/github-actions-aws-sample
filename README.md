# サンプルアプリケーション

静的なフロントエンドと Web API から成る、足し算アプリケーションです。

## 開発モードでの起動手順

サンプルアプリケーションは、以下の手順で開発モードで起動します。

```console
cd backend/
npm ci
npm run dev
```

起動したら、ブラウザで http://localhost:8080 にアクセスしてください。

Cloud9 の場合は、「Tools」>「Preview」>「Preview Running Application」でプレビューを起動して、「Pop Out Into New Window」でブラウザの別タブでアクセスしてください。

## バックエンドをビルドして実行する手順

バックエンドをビルドして実行する場合は、以下のコマンドを実行してください。

```console
cd backend/
npm ci
npm run build
node dist/index.js
```

## GitHub Actions での自動デプロイ用 IAM Role のカスタム信頼ポリシー

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Federated": "<作成したIDプロバイダのARN>"
      },
      "Action": "sts:AssumeRoleWithWebIdentity",
      "Condition": {
        "StringEquals": {
          "token.actions.githubusercontent.com:aud": "sts.amazonaws.com",
          "token.actions.githubusercontent.com:sub": "repo:<GitHubの組織またはアカウント名>/<GitHubのリポジトリ名>:ref:refs/heads/main"
        }
      }
    }
  ]
}
```
