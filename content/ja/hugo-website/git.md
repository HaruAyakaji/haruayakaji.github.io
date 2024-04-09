+++
title = 'Git 基本操作コマンド'
weight = 2
+++

## Git 基本操作

### プロジェクトの初期化

名前とメールを設定する必要があります。`--global` を使用すると、同じデバイスで一度だけ設定すればよいです。

```sh
git config --global user.name "<userName>"
git config --global user.email "<userEmail>"
git init
```

### ステージングエリア (staging area)

変更をコミットする前にファイルをステージングエリアに追加する必要があります。

```sh
# 特定のファイルをステージングエリアに追加する
git add <fileName>

# すべてのファイルをステージングエリアに追加する (.gitignore で設定された内容を除く)
git add .

# 特定のファイルをステージングエリアから削除する
git rm --cached <fileName>
```

### 変更をコミット (commit)

```sh
git commit -m "<message>"
```

### コミットの取り消し (reset)

コミットを取り消したい場合は、 `git reset` コマンドを使用します。
このコマンド自体も `git reset` を使って一度に取り消すことができます。

{{< tabs >}}
{{% tab title="mixed mode" %}}

```sh
# commit hash 値を確認する
git reflog

# コミットを取り消す (作業ディレクトリのファイルは変更されません)
git reset <commitHash>
```

{{% /tab %}}
{{% tab title="hard mode" %}}

```sh
# commit hash 値を確認する
git reflog

# コミットを取り消す (作業ディレクトリのファイルも変更されます)
git reset <commitHash> --hard
```

{{% /tab %}}
{{< /tabs >}}

## Git 上級操作

### ブランチの切り替え (branch)

```sh
# ブランチの作成
git branch <branchName>

# ブランチの削除
git branch -d <branchName>

# ブランチの切り替え
git checkout <branchName>

# ブランチのマージ
git merge <branchName>
```

{{% notice style="warning" title="衝突の解決" icon="exclamation-circle" %}}

1. 通常、新しいプロジェクトを開発する場合は新しいブランチを作成して開発します。
2. 開発が完了したら、main ブランチに戻り、dev ブランチを main ブランチにマージする。
3. マージ時に衝突が発生した場合は、手動で解決する必要があります (VSCode の補助を利用できます)。
4. 衝突の解決が完了したら、 `git add` と `git commit`を再度行う必要があります。

{{% /notice %}}

## GitHub

### SSH キーの作成

```sh
# GitHub に SSH キーを生成してコピーします
ssh-keygen
cat ~/.ssh/id_rsa.pub
```

### リモートリポジトリへのプッシュ

```sh
git remote add origin <remoteURL>
git push -u origin main
```

### リモートリポジトリからローカルへのダウンロード

```sh
# ローカルにリポジトリがない場合に使用します
git clone <remoteURL>

# リモートリポジトリの最新の状態をローカルに反映します
git pull <remoteURL>
```

{{% notice style="warning" title="衝突の解決" icon="exclamation-circle" %}}

1. 同期の過程で衝突が発生した場合は、手動で解決する必要があります (VSCode の補助を利用できます)。
2. 衝突の解決が完了したら、 `git add` と `git commit`を再度行う必要があります。

{{% /notice %}}
