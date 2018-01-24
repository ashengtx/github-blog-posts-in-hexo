---
title: Use-Hexo
date: 2017-08-28 20:09:44
tags: others
---
### 1 新建一篇文章

```
$ hexo new post use-hexo.md
```

### 2 启动服务器

#### 2.1 安装hexo-server
```
$ npm install hexo-server --save
```

#### 2.2 启动server
```
$ hexo server 
```
便可以在浏览器中访问 'http://localhost:4000/' 看到自己的博客

#### 2.3 指定端口启动server
```
$ hexo server -p 5000
```
有时候默认端口访问不了，可以换个端口。如果chrome使用了代理，也会导致本地访问不了，关掉就行了，或者换ie访问也行。


### 3 生成静态文件

#### 3.1 生成静态文件
```
$ hexo generate
```

#### 3.2 查看文件变化
```
$ hexo generate --watch
```

### 4 布署到git

#### 4.1 安装git
```
$ npm install hexo-deployer-git --save
```

#### 4.2 配置

编辑 '_config.yml' 文件
```xml
deploy:
  type: git
  repo: https://github.com/you/you.github.io
  branch: [branch]
  message: [message]
```

#### 4.3 布署
```
$ hexo deploy
```

#### 4.4 生成布署两步可以合起来
```
$ hexo generate --deploy
```

### 5 主题

看中一个主题[yilia](https://github.com/litten/hexo-theme-yilia),安装配置见其github

#### 5.1 设置头像

将头像文件 avatar.jpg 放到 /hexo/public/img 目录，然后在 yilia 的 _config.yml 文件里修改
```
#你的头像url
avatar: /img/avatar.jpg
```

#### 5.2 添加评论

目前比较好用的是disqus，但是需要翻墙。

去[disqus](https://disqus.com/)注册，然后创建一个site，配置disqus的时候，主要就填两个东西
```
Website Name: [yourname]
Website URL: [yourUrl] or [yourname].github.io
```

然后在 yilia 的 _config.yml 文件里修改
```
disqus: [yourname]
```

然后生成布署就可以看到了，前提是有代理，否则看不到评论的模块。


