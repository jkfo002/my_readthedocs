# git

## 一些常用的git还有踩过的坑

- 配置用户名与邮箱，用户名与git账号相同，邮箱类似。

  在最开始配置即可，后面就不用二次配置，可更改（~~坑+1~~）

  ```shell
  git config --global user.name "GitHub用户名"
  git config --global user.email "注册GitHub用的邮箱"
  ```

- ssh key

  ```shell
  ssh-keygen -t rsa -C "注册GitHub用的邮箱"
  ```

  生成ssh key，需要在账户中的`Settings`的`SSH and GPG keys`添加`SSH keys` 随便起个名字就可以

- 远程创建仓库

  `git@github.com/<username>/<repositeriename>`

- 链接远程仓库

  ```shell
  git init
  git add .
  git commit -m "提交信息"
  git remote add origin git@github.com/<username>/<repositeriename>
  git push -u origin main
  ```

  `这个main即分支，后面的一些对于分支的操作要指定分支名称，网上很多命令使用master，要确定`

- 后续更新

  ```shell
  # (添加/更改文件文件)
  git status #(查看状态 是否需要更新)
  git add .
  git commit -m "add readthedocs.yaml"
  git push 
  ```

  当你的远程仓库出现过其他更新的时候，需要先fetch(~~坑+1~~)，之前在网站点了`add Readme.md`，折腾了好久

  ```shell
  git fetch origin main #(当远程git与本地git不同使用)
  git merge main #(与本地进行合并)
  ```

## 其他坑欢迎分享

有空会更新，或者直接pull requset

`https://github.com/jkfo002/my_readthedocs/issues`