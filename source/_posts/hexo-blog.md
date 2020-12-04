---
title: hexo-blog
---

# hexo
> 简单

安装hexo脚手架

```javascript
npm i -g hexo-cli
```

进行hexo初始化

```javascript
hexo init 项目名称
```

初始化得到项目,重要目录介绍

| scaffolds                            | md模板       |
| ------------------------------------ | ------------ |
| sourse/_posts                        | 文章和页面md |
| themes/landscape                     | 主题样式     |
| /themes/landscape/sourse/_config.yml | 主题相关配置 |
| _config.yml                          | hexo应用配置 |

启动服务

```javascript
hexo server
```

下载一个喜欢的主题

```javascript
git clone https://github.com/probberechts/hexo-theme-cactus.git themes/cactus

```

删除cactus文件夹中的.git，删除整个原生主题文件夹，在项目根目录_config.yml中修改主题





## 在github中部署

初始化

```javascript
git init
```

安装hexo和git的依赖包

```javascript
npm i hexo-deployer-git
```

连接远程仓库

```javascript
git remote add origin git@github.com:shyboy2020/shyboy2020.github.io.git

```

在根目录下_config.yml中的添加

```javascript
deploy:
  type: git
  repo: https://github.com/shyboy2020/shyboy2020.github.io
  branch: master
```

部署代码(提交的其实是项目中的public文件夹)

```javascript
hexo deploy
```



## 自动化部署

> 不需要本地代码打包、部署
>
> 直接修改博客之后，提交代码就可以了

建立新分支myblog

添加代码

```javascript
git add .
```

commit 

```javascript
git commit -m "."
```

上传到分支

```javascript
git push --set-upstream origin myblog
```



在项目中创建.github文件夹，在该文件夹下创建workflows文件夹，创建deploy.yml文件

配置deploy.yml

```javascript
name: Build and Deploy
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout 🛎️
        uses: actions/checkout@v2 # If you're using actions/checkout@v2 you must set persist-credentials to false in most cases for the deployment to work correctly.
        with:
          persist-credentials: false

      - name: Install and Build 🔧 # This example project is built using npm and outputs the result to the 'build' folder. Replace with the commands required to build your project, or remove this step entirely if your site is pre-built.
        run: |
          npm install
          npm run build
        env:
          CI: false

      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@releases/v3
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          BRANCH: master # The branch the action should deploy to.
          FOLDER: public # The folder the action should deploy.
```



之后就可以在本地修改博客



之后提交代码 git add .    git commit -m "..."  git push 就可以了





