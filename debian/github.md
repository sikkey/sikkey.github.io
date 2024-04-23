# github-cli

## github-cli 安装

```bash
sudo apt update
sudo apt install gh
```

## github-cli 配置

```bash
gh auth login
```

或

```bash
gh auth login --web
```

或

```bash
gh auth login --with-token < mytoken.txt
```

## github-cli 使用

创建一个新的仓库

```bash
gh repo create
```

## github-cli 帮助

```bash
gh help
```

## github-cli 常用命令

| 命令 | 描述 | 语法 | 详细 |
|---|---|---|---|
| `gh repo create` | 创建新仓库 | `gh repo create [--public] [--private] [--internal] [--clone] [--source .] [--push]` | - `--public`: 创建公开仓库<br>- `--private`: 创建私有仓库<br>- `--internal`: 创建内部仓库（组织内可见）<br>- `--clone`: 克隆新创建的仓库到本地<br>- `--source .`: 从现有本地目录创建仓库（推送本地文件）<br>- `--push`: 将现有本地提交推送到新创建的远程仓库 |
| `gh repo clone` | 克隆现有仓库到本地 | `gh repo clone <repository-URL>` 或 `gh repo clone <organization>/<repository-name>` | |
| `gh repo view` | 查看仓库信息 | `gh repo view <repository-URL>` 或 `gh repo view <organization>/<repository-name>` | |
| `gh repo fork` | 创建现有仓库的副本（fork） | `gh repo fork <repository-URL>` 或 `gh repo fork <organization>/<repository-name>` | |
| `gh repo list` | 列出您的个人仓库和您所在组织的仓库 | `gh repo list [--all] [--org]` | - `--all`: 列出所有仓库（包括私有仓库）<br>- `--org`: 列出特定组织的仓库 |
| `gh repo delete` | 删除现有仓库（谨慎使用！） | `gh repo delete <repository-URL>` 或 `gh repo delete <organization>/<repository-name>` | |
| `gh repo transfer` | 将仓库所有权转让给另一用户或组织 | `gh repo transfer <repository-URL> <new-owner>` | |
| `gh repo rename` | 重命名现有仓库 | `gh repo rename <repository-URL> <new-name>` | |
| `gh repo create-from` | 从模板仓库创建新仓库 | `gh repo create-from <template-repository-URL> <new-repository-name>` | |
| `gh repo create-for-org` | 在特定组织内创建新仓库（需要组织成员权限并具有创建仓库权限） | `gh repo create-for-org <organization> <repository-name>` | |
| `gh repo create-for-team` | 在组织内特定团队内创建新仓库（需要团队成员权限并具有创建仓库权限） | `gh repo create-for-team <organization> <team-slug> <repository-name>` | |
| `gh repo set-remote-url` | 更改现有本地 Git 仓库的远程 URL（用于将其指向不同的 fork 或镜像） | `gh repo set-remote-url <repository-URL> <new-remote-URL>` | |
| **提交代码** | 将本地代码更改提交到暂存区 | `git add <file-pattern>` 或 `git add .` | - `<file-pattern>`: 指定要添加的文件或目录模式<br>- `.`: 添加所有已跟踪的文件 |
| | 将暂存区中的更改提交到本地仓库 | `git commit [-m "<commit-message>"]` | - `-m "<commit-message>"`: 指定提交消息 |
| | 将所有已跟踪的文件添加到暂存区并提交到本地仓库 | `git commit -a [-m "<commit-message>"]` | - `-m "<commit-message>"`: 指定提交消息 |
| **推送** | 将本地提交推送到远程仓库 | `git push` 或 `git push <remote-name>` | - `<remote-name>`: 指定要推送到哪个远程仓库（默认 `origin`） |
| | 将远程仓库的最新更改合并到本地分支 | `git merge <remote-branch>` 或 `git merge origin/<remote-branch>` | - `<remote-branch>`: 指定要合并的远程分支（默认 `origin/master`） |
| **切换branch** | 切换到另一个分支 | `git checkout <branch-name>` | - `<branch-name>`: 指定要切换到的分支名称 |
| **更新代码** | 从远程仓库拉取最新代码 | `git fetch` | 从远程仓库下载最新数据，但不会将远程更改合并到本地分支。|
| **同步** | 将本地分支与远程分支同步 | `git pull` | 先执行 git fetch，然后将远程更改合并到本地分支。 |

**附加命令:**

* `git branch`: 列出本地分支
* `git branch -r`: 列出远程分支
* `git branch -a`: 列出所有本地和远程分支
* `git status`: 查看当前仓库状态
* `git log`: 查看提交历史记录
* `git diff`: 查看代码更改
* `git reset`: 撤销提交或重置代码
* `git tag`: 创建、列出和删除标签
* `git remote`: 管理远程仓库
* `git commit --amend`: 修改最新提交

**注意:** 这些命令需要您已安装并使用 GitHub 帐户身份验证了 GitHub CLI。

**建议:**

* 使用 `git add` 和 `git commit` 提交代码时，养成编写清晰简洁的提交消息的习惯，以便更好地跟踪代码更改历史。
* 定期从远程仓库拉取最新代码，确保您的本地代码与远程代码保持同步。
* 在切换分支之前，请确保您的本地代码已提交并与远程代码同步。
* 使用 `git status` 和 `git diff` 命令定期检查您的代码状态和更改。


