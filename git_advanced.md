## 一、Git 四个核心区域（基础原理）
Git 的文件流转分为四块
1. **工作区（Working Directory）**：电脑上能直接看见、用 Typora / 记事本编辑的文件夹文件。
2. **暂存区（Staging Area）**：`git add` 之后文件放到这里，是一个临时中转站，标记哪些内容准备提交。
3. **本地版本库（Local Repository）**：`git commit` 之后，Git 在本地生成一份永久快照，记录当前版本，存在 `.git` 隐藏文件夹里。
4. **远程仓库（Remote Repository）**：GitHub 服务器上的仓库，`git push` 把本地版本上传上去。

流转顺序：
**工作区 →（git add）→ 暂存区 →（git commit）→ 本地仓库 →（git push）→ 远程仓库**

## 二、基础提交流程
```bash
# 1. 进入本地仓库文件夹
cd /c/你的本地仓库路径/Tasks

# 2. 初始化Git仓库（仅第一次新建仓库执行，后续不用重复）
git init

# 3. 将指定文件加入暂存区
git add hello.md
# 批量把所有改动文件加入暂存区（谨慎使用）
# git add .

# 4. 提交到本地版本库，备注要写清楚改动内容
git commit -m "add hello.md 完成阶段二hello文件"

# 5. 关联远程仓库，只需要执行一次
git remote add origin https://github.com/duxinyu1234/Tasks.git

# 6. 推送到远程main分支
git push origin main
 GitHub 默认分支名字大多是 main，老教程会写 master，不能混用。