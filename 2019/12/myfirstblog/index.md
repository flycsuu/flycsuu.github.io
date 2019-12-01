# Win10快速搭建个人博客 Hugo+gihub & hugo+码云

Hugo + github 或 hugo + 码云 搭建个人博客

<!--more-->

## 1. Hugo安装

主要参考hugo[官网链接](https://www.gohugo.org/)，需要本机预装[git](https://git-scm.com/)。
### 快速安装
- windows可直接在github下载对应的版本的[hugo](https://github.com/gohugoio/hugo/releases)到本地文件夹下；
- 解压hugo文件夹，例如解压到：D:\myblog\hugo；
- 添加系统变量；
右键我的电脑 -> 高级系统设置 -> 环境变量 -> 系统变量(Path) -> 添加hugo路径；
```
# 以D盘举例
D:\myblog\hugo
```
- 新建站点
win+r 打开运行窗口输入cmd打开命令窗口，进入hugo文件目录，生成站点。
```
$ hugo new site D:\myblog\site
```
### 新建文章
- 创建第一篇博客
```
$ hugo new posts\myfirstblog.md
```
### 主题选择
- 到hugo体统的[主题列表](https://themes.gohugo.io/)中选择一款自己心仪的主题。自己选择的是一款比较简洁的[LoveIt](https://github.com/dillonzq/LoveIt)主题。
- 主题安装
命令行进入主题目录下，从github上clone自己选择的主题。
```
$ cd themes
$ git clone https://github.com/dillonzq/LoveIt.git
```
主题clone完后记得修改hugo站点配置文件，在根目录下修改对应的配置文件config.toml。通常下载好的主题会有参样例（我这样懒人的福音）exampleSite文件夹，对应着修改，如果没有样例的话就好好阅读README.MD文件吧\表情。
### 站点本地调试
- 在根目录下执行以下命令进行调试，以LoveIt主题为例；
```
$ hugo server --theme=Loveit --buildDrafts
```
命令窗口提示使用浏览器打开http:\\\localhost:1313进行预览。（如果预览失败，查看下配置文件config.toml是否正确）
## 2. Github 部署
- 在Github上创建仓库(Repository),命名为：[flycsuu.github.io](https://flycsuu.github.io/)(flycsuu替换为自己的Github用户名，都为小写字符)

- 在根目录下执行以下命令(Url替换为自己的地址)；
```
$ hugo --theme=LoveIt --baseUrl="https://flycsuu.github.io/" --buildDrafts
```
一切顺利，会生成一个public文件夹，将该文件夹内的所有文件push到刚刚创建的Github仓库中(Repository)。
```
$ cd public
$ git init
$ git remote add origin https://github.com/flycsuu/flycsuu.github.io
$ git add -A
$ git commit -m "commit for github"
$ git push -u origin master
```
- 浏览器访问[https://flycsuu.github.io/](https://flycsuu.github.io/)就会看到刚刚搭建的博客站点。
## 3. 码云(Gitee)配置
码云(Gitee)博客网站的搭建基本于Github一致，一点点的出处在于仓库站点的创建。
### 创建仓库
需要创建一个同名仓库，这里以fucs为例。（注意仓库不能为空，空仓库没有Pages选项）
![creat](https://github.com/flycsuu/flycsuu.github.io/raw/master/img/myfirstblog/creat.png)

### 启动服务
点击服务 -> 服务 -> Pages -> 强制HTTPS -> 启动服务；
- 点击服务，选择Pages 
![service](https://github.com/flycsuu/flycsuu.github.io/raw/master/img/myfirstblog/service.png)
- 点击启动
![start](https://github.com/flycsuu/flycsuu.github.io/raw/master/img/myfirstblog/start.png)
- 启动成功后会生成自己站点的url，如：[https://fucs.gitee.io/](https://flycsuu.github.io/)
![started](https://github.com/flycsuu/flycsuu.github.io/raw/master/img/myfirstblog/started.png)
- （非必要）手动删除code下的两个README.MD文件;
### 站点部署
- 重新生成站点文件(Url替换为码云地址)
```
$ hugo --theme=LoveIt --baseUrl="https://fucs.gitee.io/" --buildDrafts
```
- 将本地站点下的public文件夹下的内容推送到码云仓库中；
```
$ cd public 
$ git remote add origin2 https://gitee.com/fucs/fucs.git
$ git add .
$ git commit -m "commit for gitee"
$ git push -u origin2 master
```
- 此时可能出现 err 如下,原因是远程仓库与本地仓库不一致所造成的
![err](https://github.com/flycsuu/flycsuu.github.io/raw/master/img/myfirstblog/err.png)
- 此时需要远程同步到本地仓库
```
$ git pull --rebase origin2 master
```
- 实践时发现此处需要重启服务
![started](https://github.com/flycsuu/flycsuu.github.io/raw/master/img/myfirstblog/restart.png)
- 浏览器访问[https://fucs.gitee.io/](https://fucs.gitee.io/)就会看到刚刚搭建的博客站点。
## 4. 图片显示问题
还没明白如何使用框架在博客中插入图片，暂时的解决方案是直接应用github或码云的图片链接，有时间再继续研究。不过直接引用的话需要修养引用链接，需要将blob修改掉。
```
https://gitee.com/fucs/fucs/blob/master/img/myfirstblog/xxx.png
# 修改为
https://gitee.com/fucs/fucs/raw/master/img/myfirstblog/xxx.png
```