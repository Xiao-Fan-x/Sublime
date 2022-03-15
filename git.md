# 配置文件

windows本机：C:\ProgramData\Git\config

系统用户级别：登录当前操作系统的用户范围

git config --global user.name XXX

git config --global user.email XXX@XXX

列出所有Git的配置：

git config --list

git config <key> 检查Git的某一项（key）配置

查看Git配置的所在文件：

git config --show-origin + <key>

git config --show-origin user.name file:C:/Users/Xiaofan/.gitconfig Xiao-Fan-x

文本编辑器
git config --global core.editor emacs


# 获取帮助

$ git help <verb>
$ git <verb> --help $ man git-<verb>

快速参考：

git -h

```shell
git add -h
usage: git add [<options>] [--] <pathspec>...
-n, --dry-run         dry run
-v, --verbose         be verbose

-i, --interactive     interactive picking
-p, --patch           select hunks interactively
-e, --edit            edit current diff and apply
-f, --force           allow adding otherwise ignored files
-u, --update          update tracked files
--renormalize         renormalize EOL of tracked files (implies -u)
-N, --intent-to-add   record only the fact that the path will be added later
-A, --all             add changes from all tracked and untracked files
--ignore-removal      ignore paths removed in the working tree (same as --no-all)
--refresh             don't add, only refresh the index
--ignore-errors       just skip files which cannot be added because of errors
--ignore-missing      check if - even missing - files are ignored in dry run
--chmod (+|-)x        override the executable bit of the listed files
--pathspec-from-file <file>
                      read pathspec from file
--pathspec-file-nul   with --pathspec-from-file, pathspec elements are separated with NUL character
```

开始跟踪文件 / 将文件放入暂存区：git add + 文件

git add 命令使用文件或目录的路径作为参数；如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。

git add 将修改的文件载入暂存区

| git status -s           |                          |
| ----------------------- | ------------------------ |
| M README                | 工作区已修改但未暂存     |
| MM Rakefile             | 文件已修改，暂存后又修改 |
| A      lib/git.rb       | 新添加到暂存区           |
| M      lib/simplegit.rb | 已修改已暂存             |
| ?? LICENSE.txt     | 新添加未跟踪             |

将文件从暂存区中撤下： git rm --cached + 文件  (文件仍保留在当前工作目录中，但从 Git 仓库中删除，不让 Git 继续跟踪)

查看工作区、暂存区状态：git status

https://github.com/github/gitignore

文件改名操作：git mv file_from file_to

git mv 相当于运行了下面三条命令

$ mv README.md README

$ git rm README.md

$ git add README



查看提交历史：git log

git log 会按时间先后顺序列出所有的提交，最近的更新排在最上面

git log -p/-patch 现实最近p次的提交

git log --stat 详细显示修改过的文件内容


git log --pretty= {} oneline/short/full/fuller/format:"%h - %an, %ar : %s"

format 常用的选项
选项 说明
%H 提交的完整哈希值
%h 提交的简写哈希值
%T 树的完整哈希值
%t 树的简写哈希值
%P 父提交的完整哈希值
%p 父提交的简写哈希值
%an 作者名字
%ae 作者的电子邮件地址
%ad 作者修订日期（可以用 --date=选项 来定制格式）
%ar 作者修订日期，按多久以前的方式显示
%cn 提交者的名字
%ce 提交者的电子邮件地址
%cd 提交日期
%cr 提交日期（距今多长时间）
%s 提交说明

--graph 显示ascii分支信息

 git log 的常用选项
选项 说明
-p 按补丁格式显示每个提交引入的差异。
--stat 显示每次提交的文件修改统计信息。
--shortstat 只显示 --stat 中最后的行数修改添加移除统计。
--name-only 仅在提交信息后显示已修改的文件清单。
--name-status 显示新增、修改、删除的文件清单。
--abbrev-commit 仅显示 SHA-1 校验和所有 40 个字符中的前几个字符。
--relative-date 使用较短的相对时间而不是完整格式显示日期（比如“2 weeks ago”）。
--graph 在日志旁以 ASCII 图形显示分支与合并历史。
--pretty 使用其他格式显示历史提交信息。可用的选项包括 oneline、short、full、fuller 和
format（用来定义自己的格式）。
--oneline --pretty=oneline --abbrev-commit 合用的简写。


git log 输出的选项
选项 说明
-<n> 仅显示最近的 n 条提交。
--since, --after 仅显示指定时间之后的提交。
--until, --before 仅显示指定时间之前的提交。
--author 仅显示作者匹配指定字符串的提交。
--committer 仅显示提交者匹配指定字符串的提交。
--grep 仅显示提交说明中包含指定字符串的提交。
-S 仅显示添加或删除内容匹配指定字符串的提交。

 git commit --amend
将暂存区中的文件提交，第二次提交将代替第一次提交的结果
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend

取消暂存的文件  撤销git add
git reset HEAD <file>


撤销对文件的修改
git checkout -- <file>...
表示将在工作空间但是不在暂存区的文件撤销更改
git restore <file>


作用是将暂存区的文件从暂存区撤出，但不会更改文件
git restore --staged <file>


切换到本地的分支
git checkout testing



git checkout -b iss53

$ git branch iss53
$ git checkout iss53



git merge 新的分支 ： 将指针从当前移到完全新增内容的新分支

删除分支
 git branch -d + 分支


### 遇到冲突时的分支合并
任何因包含合并冲突而有待解决的文件，都会以未合并状态标识出来


查看暂存区文件
git ls-files

查看哪些分支已经合并到当前分支
git branch --merged
查看所有包含未合并工作的分支
git branch --no-merged

切换远程的origin/serverfix分支映射成本地的sf分支
git checkout -b sf origin/serverfix

变基
$ git checkout A
$ git rebase master
切换到A 分支，将A的操作，再master 上再做一遍
$ git checkout master
$ git merge A