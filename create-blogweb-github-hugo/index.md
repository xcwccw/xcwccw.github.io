# Create BlogWeb Github Hugo


# github+Hugo搭建博客

## 1.安装

1. 前往[Releases · gohugoio/hugo (github.com)](https://github.com/gohugoio/hugo/releases)下载对应版本的hugo，建议下载扩展版，因为很多主题的内容需要基于扩展版之上才有用，不是扩展版会报错。
2. 将下载好的hugo压缩包解压至指定文件夹中，解压路径中不要出现中文和空格。
3. 将解压出来的hugo.exe的存放路径添加至环境变量。
4. 验证：打开cmd，运行hugo help，如果屏幕输出了hugo相关的命令指导说明安装成功！



## 2.创建站点

```
站点的本质其实就是"装有很多其它文件夹/文件的"文件夹

# 创建站点的指令
$ hugo new site 站点名(比如说:MyBlog)

# 进入站点
$ cd MyBlog
```



## 3.设置主题

1. 下载主题：[Complete List | Hugo Themes (gohugo.io)](https://themes.gohugo.io/)，先去挑选一个自己喜欢的主题，然后打开，点击黄色的Downlord按钮，就会跳转到该主题对应的github项目处，然后我们复制该主题github项目对应的https下载网址，然后执行以下操作：

```
# 先进入站点根目录下的themes文件夹中(此前我们已经进入了站点文件夹中，已经处于站点根目录下)
$ cd themes

# 下载主题对应的github项目到themes文件夹下
$ git clone 主题对应的github项目的https下载路径
```

2. 对站点根目录下的配置文件(hugo.toml)进行配置：

```
# 原本就有的：
baseURL = 'https://example.org/' 我们先进行本地部署，所以这个可以先不修改
languageCode = 'en-us'
title = 'My New Hugo Site'
# 额外添加的
theme = "主题名" # 就是themes文件夹中下载好的主题的文件夹名(比如"LoveIt")
```



## 4.创建文章

```
# 创建一个about页面
# about.md自动生成到了content/about.md
$ hugo new about.md 

# 创建一个first页面，放到post目录下，方便之后聚合页面
# first.md自动生成到了content/post/first.md
$ hugo new post/first.md

# 创建的md文件中的内容
+++
date = "2023-9-3T18:36:54-07:00"
draft = true # 是否为草稿内容
title = "about"

+++

正文内容
```



## 5.本地启动hugo服务

```
# --themes=hyde 指定构建网页使用的主题
# --BuildDrafts 指定草稿也会被构建
$ hugo server --themes=hyde --BuildDrafts
$ hugo serve -e production --本地服务开启评论系统

# 然后打开其指定的本地网址即可访问博客了
http://localhost:1313/
```



## 6.托管到github上

* 警告：github上使用的博客托管仓库，即：用户名.github.io这个仓库，必须是全新的，如果之间用于其它框架搭建博客需要删除重新创建，建议这样做，否则后期部署可能会出现奇怪的错误

```
# 在站点根目录下进行操作:

# 生成对应的public文件夹，里面装的就是要发布的博客网页(md->html)
$ hugo

# 进入public文件夹
$ cd public

# 将public文件夹作为一个本地git仓库，先初始化本地git仓库
$ git init 

# 将public问价夹下的所有文件追加到本地仓库
$ git add . 

# 将上面执行的add操作进行提交
$ git commit -m "first commit" 

# 将本地仓库和远程仓库相互关联
$ git remote add origin https://github.com/xcwccw/xcwccw.github.io.git 
# 如果关联到错误的地址:
$ git remote -v # 查看当前关联的远程仓库地址
$ git remote rm origin # 移除当前关联的远程仓库地址

# 将本地仓库的文件推送到远程仓库进行托管，不行用下面这个
$ git push -u origin master 
# 强制推送
$ git push -f origin master 

-- 之后要写了新的博客要更新内容只需要执行以下操作即可(可以写个脚本)
$ hugo
$ cd public
$ git add .
$ git commit -m "first commit"
$ git push -u origin master
```



## 7.配置评论系统

1. 创建一个公开的 Github 仓库

2. 找到`Settings -> General -> Features -> Discussions` 勾选，为仓库启动 Discussions 功能

3. 给配置好的仓库安装Giscus，点击[GitHub Apps - giscus](https://github.com/apps/giscus)，点击Install

4. 点击Install后，要选择一个git仓库进行安装

5. 接下来，我们只需到 Giscus 官网获取配置信息，然后将配置信息填到 Hugo 的[配置文件](https://www.zhihu.com/search?q=配置文件&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A3115481653})中即可。但是由于主题的不同，所以配置文件的填写也不同，这里以 LoveIt 为例。

6. 来到 [Giscus 官网](https://link.zhihu.com/?target=https%3A//giscus.app/zh-CN)；填写你的git仓库名：xcwccw/Giscus；选择页面与嵌入的discussion之间的映射关系为Discussion的标题包含页面的pathname项；选择 Discussion 分类，我们选择 Announcements 类型即可，官方也是这样推荐的，因为这样便于管理；其他选项默认，我们往下滑，找到配置文件，我们要记下`data-repo`，`data-repo-id`，`data-category`，`data-category-id`，`data-mapping`这几个值。

7. 打开配置文件`config.toml`，找到`# 评论系统设置`的第一个 enable 参量，将其改为 true

8. 找到`# giscus comment 评论系统设置`,并把其配置按照下面代码块修改。

```yaml
[params.page.comment.giscus]   
  # 你可以参考官方文档来使用下列配置   
  enable = true   
  repo = "<your_repo>"   
  repoId = "<your_repoId>"   
  category = "<your_category>"   
  categoryId = "<your_categoryId>"   
  # <your_repo> 对应官网的 data-repo   
  # <your_repoId> 对应官网的 data-repo-id   
  # <your_category> 对应官网的 data-category   
  # <your_categoryId> 对应官网的 data-category-id

  # 为空时自动适配当前主题 i18n 配置   
  lang = "zh-CN"   
  mapping = "<your_mapping>"   
  # <your_mapping> 对应官网的 data-mapping   
  reactionsEnabled = "1"   
  emitMetadata = "0"   
  inputPosition = "bottom"   
  lazyLoading = false   
  lightTheme = "light"   
  darkTheme = "dark_dimmed"
```

9. 配置好后,就可以开启 Giscus 评论系统了。



## 8.其它内容

### 8.1.测试-测试

测试测试

