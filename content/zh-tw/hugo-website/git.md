+++
title = 'Git 基本操作指令'
weight = 2
+++

## Git 基本操作

### 初始化專案

名稱和信箱必須設定，若使用 `--global` 套用在同一部裝置上則只需要設定一次。

```sh
git config --global user.name "<userName>"
git config --global user.email "<userEmail>"
git init
```

### 暫存區 (staging area)

提交變更之前需要先將檔案新增至暫存區。

```sh
# 將特定檔案加入到暫存區
git add <fileName>

# 將所有檔案加入到暫存區 (排除 .gitignore 設定的內容)
git add .

# 將特定檔案從暫存區移除
git rm --cached <fileName>
```

### 提交變更 (commit)

```sh
git commit -m "<message>"
```

### 提交反悔 (reset)

想要撤銷提交可以使用 `git reset` 指令，此指令本身也可以在一次使用 `git reset` 撤銷。

{{< tabs >}}
{{% tab title="mixed mode" %}}

```sh
# 查詢 commit hash 值
git reflog

# 撤銷提交 (工作目錄的檔案不會被改變)
git reset <commitHash>
```

{{% /tab %}}
{{% tab title="hard mode" %}}

```sh
# 查詢 commit hash 值
git reflog

# 撤銷提交 (工作目錄的檔案會被改變)
git reset <commitHash> --hard
```

{{% /tab %}}
{{< /tabs >}}

## Git 進階操作

### 切換分支 (branch)

```sh
# 建立分支
git branch <branchName>

# 刪除分支
git branch -d <branchName>

# 切換分支
git checkout <branchName>

# 合併分支
git merge <branchName>
```

{{% notice style="warning" title="衝突處理" icon="exclamation-circle" %}}

1. 一般的情況，開發新項目會建立新的分支來開發。
2. 開發完成時，會切換回 main 分支，將 dev 分支合併到 main 分支。
3. 如果在合併時發生衝突，則必須手動解決衝突 (可以依賴 VSCode 的輔助)。
4. 衝突解決完成時，必須重新 `git add` 和 `git commit`。

{{% /notice %}}

## GitHub

### 建立 SSH Key

```sh
# 產生 SSH Key 之後複製到 GitHub
ssh-keygen
cat ~/.ssh/id_rsa.pub
```

### 推送到遠端儲存庫

```sh
git remote add origin <remoteURL>
git push -u origin main
```

### 從遠端儲存庫下載到本地端

```sh
# 當本地端沒有儲存庫時使用
git clone <remoteURL>

# 將遠端儲存庫的最新狀態反映到本地端
git pull <remoteURL>
```

{{% notice style="warning" title="衝突處理" icon="exclamation-circle" %}}

1. 如果在同步的過程中發生衝突，則必須手動解決衝突 (可以依賴 VSCode 的輔助)。
2. 衝突解決完成時，必須重新 `git add` 和 `git commit`。

{{% /notice %}}
