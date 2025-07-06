# Git/GitHub チーム開発手順書

このドキュメントは、チームでGit/GitHubを使って開発を行うための基本的な手順を説明します。

## 目次
1. [リポジトリの作成](#1-リポジトリの作成)
2. [チームメンバーの招待](#2-チームメンバーの招待)
3. [リポジトリのクローン](#3-リポジトリのクローン)
4. [ブランチの作成と切り替え](#4-ブランチの作成と切り替え)
5. [ファイルの編集とコミット](#5-ファイルの編集とコミット)
6. [プルリクエストの作成](#6-プルリクエストの作成)
7. [レビューとマージ](#7-レビューとマージ)
8. [変更の取得](#8-変更の取得)

---

## 1. リポジトリの作成

### リポジトリ作成者（チームリーダー）の作業

1. GitHubにログインする
2. 右上の「+」ボタンから「New repository」を選択
3. 以下の情報を入力：
   - Repository name: `git-study`
   - Description: チームでGitを学ぶためのプロジェクト
   - Public/Private: チームの要件に応じて選択
   - Initialize with README: チェックを入れる(別に入ればくてもいい)
4. 「Create repository」をクリック

---

## 2. チームメンバーの招待

### リポジトリ作成者の作業

1. 作成したリポジトリのページで「Settings」タブを開く
2. 左メニューから「Collaborators」を選択
3. 「Add people」ボタンをクリック
4. チームメンバーのGitHubユーザー名またはメールアドレスを入力
6. 「Add [username]」をクリック

(
   7 今回のみ、先にgit cloneして、
   https://github.com/mehuu2000/git-teamからPROCEDURE.mdとapp/main.html, style.cssをコピーし、作成する。
   そして、 git add, commit, pushしておく
)

### チームメンバーの作業

1. 招待メールを確認
2. 「Accept invitation」をクリック
3. リポジトリにアクセスできることを確認

---

## 3. リポジトリのクローン

### 全メンバーの作業

1. リポジトリページで「Code」ボタンをクリック
2. HTTPSのURLをコピー
3. ターミナル（コマンドプロンプト）を開く
4. 作業したいディレクトリに移動
5. 以下のコマンドを実行：

```bash
git clone https://github.com/[username]/git-team.git
cd git-team
```

---

## 4. ブランチの作成と切り替え

### 新しい機能を開発する時の作業

1. mainブランチから新しいブランチを作成：

```bash
# mainブランチにいることを確認
git branch

# 新しいブランチを作成して切り替え
git checkout -b feature/[your-name]
```

2. ブランチが切り替わったことを確認：

```bash
git branch
```

---

## 5. ファイルの編集とコミット

### ファイルを編集してGitに記録する作業

1. main.htmlを編集
今回は、チームメンバーの中にpタグでチームメンバーの名前を記入(位置を気にしてね)

2. 変更内容を確認：

```bash
git status
```

3. 変更をステージングエリアに追加：

```bash
git add main.html
```

4. コミット（変更を記録）：

```bash
git commit -m "チームメンバーに[your-name]を追加"
```

5. リモートリポジトリにプッシュ：

```bash
git push origin feature/[your-name]
```

---

## 6. プルリクエストの作成

### 変更をmainブランチに取り込んでもらうための作業

1. GitHubのリポジトリページを開く
2. 「Pull requests」タブをクリック
3. 「New pull request」ボタンをクリック
4. 以下を設定：
   - base: `main`
   - compare: `feature/[your-name]`
5. 変更内容を確認
6. 「Create pull request」をクリック
7. タイトルと説明を入力：
   - タイトル: チームメンバーに[名前]を追加
   - 説明: どのような変更をしたか詳しく記載
8. 「Create pull request」をクリック

---

## 7. レビューとマージ

### レビュアー（他のチームメンバー）の作業

1. Pull requestsページで該当のPRを開く
2. 「Files changed」タブで変更内容を確認
3. コメントがあれば記入
4. 問題なければ「Review changes」から「Approve」を選択
5. 「Submit review」をクリック

### マージ作業（権限を持つメンバー）

1. レビューが承認されたことを確認
2. 「Merge pull request」ボタンをクリック
3. 「Confirm merge」をクリック
4. マージ完了後、ブランチを削除（消さなくてもいい、オブションです）

---

## 8. 変更の取得

### 全メンバーが最新の状態を取得する作業

1. mainブランチに切り替え：

```bash
git checkout main
```

2. 最新の変更を取得：

```bash
git pull origin main
```

3. 変更が反映されたことを確認：

---

## よく使うGitコマンド一覧

| コマンド | 説明 |
|---------|------|
| `git status` | 現在の状態を確認 |
| `git add [file]` | ファイルをステージングエリアに追加 |
| `git commit -m "message"` | コミット |
| `git push origin [branch]` | リモートにプッシュ |
| `git pull origin [branch]` | リモートから取得 |
| `git checkout [branch]` | ブランチ切り替え |
| `git checkout -b [branch]` | ブランチ作成＆切り替え |
| `git branch` | ブランチ一覧表示 |
| `git log` | コミット履歴表示 |

---

## トラブルシューティング

### コンフリクト（競合）が発生した場合

1. コンフリクトが発生したファイルを開く
2. 以下のようなマーカーを探す：
   ```
   <<<<<<< HEAD
   自分の変更
   =======
   他の人の変更
   >>>>>>> branch-name
   ```
3. どちらの変更を採用するか決めて、マーカーを削除
4. ファイルを保存
5. `git add [file]`でステージング
6. `git commit`でコミット

### プッシュできない場合

```bash
# リモートの最新を取得してから再度プッシュ
git pull origin [branch]
git push origin [branch]
```