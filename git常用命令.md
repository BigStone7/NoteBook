## git 常用命令

* **Git配置**

  系统配置：`git config  --system [配置内容] `  （作用于本操作系统，配置文件位于/etc/gitconfig）

  用户配置：`git config  --global  [配置内容]`（作用于本用户,配置文件位于用户目录./.gitconfig）

  项目配置：`git config [配置内容]` (作用于本项目，配置文件位于用项目./git/config)

  **例子**

  ```git
   git config --global user.name "John Doe"
   git config --global user.email johndoe@example.com
  ```

  **查看配置信息**

  ```git 
   git config --list
  ```

* **初始化Git仓库**

  进入你要用Git管理的仓库，执行下面的命令：

  ```git
  git init
  ```

  仓库初始化完成后会生成.git文件，里面记录了你的数据和资源。

* **将文件提交到暂存区**

  全部提交

  ```git
  git add .
  ```

  提交指定文件

  ```git
  git add [提交文件]
  ```

* **将暂存区的文件提交到本地仓库**

  ```git
   git commit -m "本次提交备注的信息"
  ```

  备注信息非常重要，可以让你看日志的时候知道具体那次的提交做了什么事。

* **配置忽略文件**

  在项目中有些文件是不需要提交到代码仓库的，我们可以通过配置`.gitignore`文件来忽略他们，如果没有该文件可以自己创建。

  `.gitignore`文件样例：

  ```shell
  # 忽略所有 .a 结尾的文件
  *.a
  
  # 但lib.a 除外
  !lib.a
  
  # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
  /TODO
  
  # 忽略 build/ 目录下的所有文件
  build/
  
  # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
  doc/*.txt
  
  # 忽略 doc/ 目录下所有扩展名为 txt 的文件
  doc/**/*.txt
  ```

* **克隆文件**

  ```git
  git clone [文件地址] [本地仓库名]
  ```

* **状态检查**

  ```git
  git status
  ```

* **差异对比**

  对比本地工作区和暂存区之间的差异

  ```git
  git diff
  ```

  对比暂存区和上次提交版本之间的差异

  ```git
  git diff --cached
  ```

* **移除文件**

  ```git
  git rm [移除文件]
  ```

* **移动文件**

  ```git
  git mv [源文件] [目标地址]
  ```

* **日志查询**

  ```git
   # 当分支版本
   git log
   
   # 日志简略信息
   git log --oneline
  
   #限制查询数量
   git log -n[数字]
   
   # 所有分支版本日志
   git log -all 
   
   #版本演变历史图形化展示
   git log --all --graph
  ```


* **文件名重命名**

  ```git
   git mv [oldName] [newName]
  ```

* **创建分支**

  ```git
   git checkout -b [分支名] [基于的版本（省略为当前分支）]
  ```

* **分支查询**

  ```git
    git branch -v
  ```

  

### git会遇到的问题

*  **分离头指针（detached HEAD)**： 指的是没有把头指针和分支绑定到一起，会造成分支切换后，数据丢失；根据提示创建新的分支就可以解决。