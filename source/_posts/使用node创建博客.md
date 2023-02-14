
---
title: 使用node—键创建博客
---
## 一.安装hexo框架

1. 安装node.js
2. 管理员身份启动命令行
3. node -v  #查看node版本 （最好是用14或者以上的版本）
4. npm -v  #查看npm版本 
5. npm install -g cnpm --registry=http://registry.npm.taobao.org  #安装淘宝的cnpm 管理器
6. cnpm -v  #查看cnpm版本
7. cnpm install -g hexo-cli  #安装hexo框架
8. hexo -v  #查看hexo版本
9.  mkdir blog  #创建blog目录
10. cd blog  #进入blog目录
    
11. ## 二.初始化博客

12. hexo init  #生成博客 初始化博客（如果windows系统创建失败，可以现用管理员身份在C:\Windows\System32中创建文件夹，之后再转移到别的文件夹中）
13. hexo s  #启动本地博客服务
14. http://localhost:4000/ #本地访问地址
15. hexo new “我的第一篇文章的名字” #创建新的文章
16. hexo clean  #清理blog文件夹缓存
17. hexo g  #生成
18. hexo s  #生成本地服务器，复制链接可以在本电脑浏览博客。
 
19. ## 二.上传部署博客 

20. 在Github创建一个新的仓库 YourGithubName.github.io (前缀名必须是你用户名，后缀必须是.github.io)
21. cnpm install --save hexo-deployer-git  #在blog目录下安装git部署插件
22. hexo c #清理一下
23. hexo g #生成
24. hexo d #部署到远程Github仓库
