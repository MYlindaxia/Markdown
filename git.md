#第一章
如果你想在克隆远程仓库的时候，自定义本地仓库的名字，你可以使用如下命令
```
$ git clone https://github.com/libgit2/libgit2 mylibgit
```
要查看哪些文件处于什么状态，可以用 git status 命令。

现在，让我们在项目下创建一个新的 README 文件。如果之前并不存在这个文件，使用 git status 命令，你将看到一个新的未跟踪文件：
```
$ echo 'My Project' > README
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    README
nothing added to commit but untracked files present (use "git add" to
track)
```
在状态报告中可以看到新建的 README 文件出现在 Untracked files 下面。未跟踪的文件意味着 Git
在之前的快照（提交）中没有这些文件；Git 不会自动将之纳入跟踪范围，除非你明明白白地告诉它“我需要跟
踪该文件”，这样的处理让你不必担心将生成的二进制文件或其它不想被跟踪的文件包含进来。不过现在的例子
中，我们确实想要跟踪管理 README 这个文件。

使用命令 git add 开始跟踪一个文件。所以，要跟踪 README 文件，运行：
```
$ git add README
```

此时再运行 git status 命令，会看到 README 文件已被跟踪，并处于暂存状态：
```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    new file: README
```

只要在 Changes to be committed 这行下面的，就说明是已暂存状态。如果此时提交，那么该文件此时此
刻的版本将被留存在历史记录中。你可能会想起之前我们使用 git init 后就运行了 git add (files) 命
令，开始跟踪当前目录下的文件。git add 命令使用文件或目录的路径作为参数；如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。

git status 命令的输出十分详细，但其用语有些繁琐。如果你使用 git status -s 命令或 git status--short 命令，你将得到一种更为紧凑的格式输出。运行 git status -s ，状态报告输出如下：
```
$ git status -s
 M README
MM Rakefile
A lib/git.rb
M lib/simplegit.rb
?? LICENSE.txt
```
新添加的未跟踪文件前面有 ?? 标记，新添加到暂存区中的文件前面有 A 标记，修改过的文件前面有 M 标记。你可能注意到了 M 有两个可以出现的位置，出现在右边的 M 表示该文件被修改了但是还没放入暂存区，出现在靠左边的 M 表示该文件被修改了并放入了暂存区。例如，上面的状态报告显示： README 文件在工作区被修改了但是还没有将修改后的文件放入暂存区,lib/simplegit.rb 文件被修改了并将修改后的文件放入了暂存区。而Rakefile 在工作区被修改并提交到暂存区后又在工作区中被修改了，所以在暂存区和工作区都有该文件被修改了的记录。

一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。在这种情况下，我们可以创建一个名为 .gitignore的文件，列出要忽略的文件模式。来看一个实际的例子：
```
$ cat .gitignore
*.[oa]
*~
```
第一行告诉 Git 忽略所有以 .o 或 .a 结尾的文件。一般这类对象文件和存档文件都是编译过程中出现的。第二行告诉 Git 忽略所有以波浪符（~）结尾的文件，许多文本编辑软件（比如 Emacs）都用这样的文件名保存副本。此外，你可能还需要忽略 log，tmp 或者 pid 目录，以及自动生成的文档等
等。要养成一开始就设置好.gitignore 文件的习惯，以免将来误提交这类无用的文件。

**GitHub 有一个十分详细的针对数十种项目及语言的 .gitignore 文件列表，你可以在https://github.com/github/gitignore 找到它.**

要查看尚未暂存的文件更新了哪些部分，不加参数直接输入 git diff：

请注意，git diff 本身只显示尚未暂存的改动，而不是自上次提交以来所做的所有改动。所以有时候你一下子暂存了所有更新过的文件后，运行 git diff 后却什么也没有，就是这个原因。

请记住，提交时记录的是放在暂存区域的快照。任何还未暂存的仍然保持已修改状态，可以在下次提交时纳入版本管理。每一次运行提交操作，都是对你项目作一次快照，以后可以回到这个状态，或者进行比较。

尽管使用暂存区域的方式可以精心准备要提交的细节，但有时候这么做略显繁琐。Git 提供了一个跳过使用暂存区域的方式，只要在提交的时候，给 git commit 加上 -a 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤：


Git 是怎么创建新分支的呢？很简单，它只是为你创建了一个可以移动的新的指针。比如，创建一个 testing分支，你需要使用 git branch 命令：
```
$ git branch testing
```

要切换到一个已存在的分支，你需要使用 git checkout 命令。我们现在切换到新创建的 testing 分支去：
```
$ git checkout testing
```

因为刚才你创建了一个新分支，并切换过去进行了一些工作，随后又切换回 master 分支进行了另外一些工作。上述两次改动针对的是不同分支：你可以在不同分支间不断地来回切换和工作，并在时机成熟时将它们合并起来。而所有这些工作，你需要的命令只有branch(创建分支)、checkout(切换分支) 和 commit(提交)

你可以运行你的测试，确保你的修改是正确的，然后将其合并回你的 master 分支来部署到线上。你可以使用git merge 命令来达到上述目的：

```
$ git checkout master
$ git merge hotfix
Updating f42c576..3a0874c
Fast-forward
 index.html | 2 ++
 1 file changed, 2 insertions(+)
```

你应该先删除 hotfix 分支，因为你已经不再需要它了 —— master 分支已经指向了同一个位置。你可以使用带 -d 选项的 git branch命令来删除分支：

```
$ git branch -d hotfix
Deleted branch hotfix (3a0874c).
```
