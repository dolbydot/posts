> 不定期补充

- 从当前分组创建新的分支：`git branch <branch>`

- 切换分支：`git checkout <branchname>`
 
- 从当前分支创建分支并切换到新建的分支：`git checkout -b <branchname>`

- 查看所有分支：`git branch --all`/`git branch -a`

- 回滚到指定的commits：`git reset --hard 完整哈希值`

- 合并指定分支到当前分支：`git merge <branchname>`

- 合并完成后删除已被合并的指定的分支：`git branch -d <branchname>`

- 合并指定的远程分支到当前分支：`git merge origin/<branchname>`
