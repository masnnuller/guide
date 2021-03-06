---
layout: main
title: 認可と認証
category: User Guide
menu: menu_ja
toc:
- title: アクセス制御
  url: "#アクセス制御"
  active: 'true'
- title: 認可
  url: "#認可"
- title: 認証
  url: "#認証"
---

# アクセス制御

アクセスをシンプルにするため、ScrewdriverはパイプラインのGitリポジトリと同じセキュリティモデルを採用しています。

## 認可

*この例ではGitHub SCMプロバイダを使用します*

Gitリポジトリ上の各自のパーミッションレベルに応じて、リンクされているScrewdriverパイプラインへのアクセス権が設定されます。

- **読み取り(ゲスト)**
    - パイプライン全体の状態を表示
    - ビルドログの表示
- **書き込み(コラボレーター)**
    - *ゲストが可能な操作*
    - 新しくビルドを開始
    - 既存のビルドを停止
- **管理(所有者)**
    - *コラボレーターが可能な操作*
    - 該当リポジトリのパイプラインの作成
    - 既存のパイプラインの削除
    - secretsの作成、更新、削除
    - ジョブの有効化と無効化

## 認証

Screwdriverが利用者のパーミッションレベルを決定するため、初回だけScrewdriverにGitアカウントをリンクする手続きを行う必要があります。これにより、Screwdriverには次の通り制限されたアクセス権が付与されます。

- **公開リポジトリへの読み取り専用アクセス** - `screwdriver.yaml`の中身を読み込むため
- **リポジトリのwebhookの完全制御** - パイプラインの作成・削除に合わせてScrewdriverのwebhookの追加・削除を行うため
- **orgとチームメンバーシップの読み取り** - 利用者のパーミッションレベルの確認（上記参照）
- **コミットステータスへのアクセス** - ビルドの成功・失敗情報でPull Requestを更新するため
