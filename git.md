# git

[TOC]

## git安装和配置

- 在Windows上安装
    1. 命令行工具：git for windows (重点) https://git-for-windows.github.io
    2. 可视化工具：TortoiseGit(了解) https://tortoisegit.org
    3. idea插件(掌握)
    4. GitHub网站(掌握) http://www.github.com
- git的配置
    - git config --global user.name ''
    - git config --global user.email ''

## git的使用

- git init：初始化版本库
- git status：查看文件状态
- git add <文件/目录名>：将文件或目录添加到临时的暂存区中
- git rm --cached <文件/目录名>：将文件或者目录移除出暂存区
- git commit：提交到本地库
    - vim编辑器编辑提示信息