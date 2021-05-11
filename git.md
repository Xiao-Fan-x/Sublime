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

git config --show-origin user.name
file:C:/Users/Xiaofan/.gitconfig        Xiao-Fan-x



# 获取帮助

$ git help <verb>
$ git <verb> --help
$ man git-<verb>

快速参考：

git  -h

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

将文件从暂存区中撤下： git rm --cached + 文件



查看工作区、暂存区状态：git status





​	

