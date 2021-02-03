## 安装gitbook
1. 安装Node.js
2. npm 安装gitbook
```
npm install gitbook-cli -g
```
## 基本使用
1. gitbook init 初始化书籍项目
```
 READEME.md 喝SUMMARY.md 是两个必须文件，READEME.md 是对书籍的介绍
 SUMMARY.md 是对书籍的目录结构
```
2. gitbook serve 编译和打包预览书籍
```
注： gitbook serve 命令实际上会首先调用gitbook build 编译书籍，完成后悔打开一个web服务器，监听在本地的4000端口
打开http://localhost:4000即可访问
```
## 目录结构
```md
* [简介](README.md)
* [一级目录](01.md)
		* [耳机目录](01.md)

```
## 插件安装
```
gitbook 还支持插件 ，可以用npm 上搜索
gitbook 的插件信息会保存在book.json中
gitbook-plugin-donate(打赏按钮): https://www.npmjs.com/package/gitbook-plugin-donate
gitbook-plugin-github-buttons(GitHub按钮): https://www.npmjs.com/package/gitbook-plugin-github-buttons
gitbook-plugin-edit-link(GitHub编辑按钮): https://www.npmjs.com/package/gitbook-plugin-edit-link
{
    "title": "gitbook",
    "description": "gitbook",
    "author": "WeiLai",
    "language": "zh-hans",
    "root": ".",

    "plugins": [
        "donate",
        "github-buttons@2.1.0",
        "edit-link"
    ],

    "pluginsConfig": {
        "donate": {
            "wechat": "https://xxx.jpg",
            "alipay": "https://xxx.jpg",
            "title": "",
            "button": "打赏",
            "alipayText": "支付宝打赏",
            "wechatText": "微信打赏"
        },
        "github-buttons": {
            "repo": "itswl/gitbook",
            "types": [
                "star"
            ],
            "size": "small"
        },
        "edit-link": {
            "base": "https://github.com/itswl/gitbook/edit/master",
            "label": "Edit This Page"
        }
    }
}
如果报错先运行gitbook install
```
## 发布
1. 在 gitbook.com 上发布和管理书籍
 - 需要先注册 gitbook 账号。可以单独注册，也可以使用 github 账号关联登录。
 - 然后先创建一个 Orgnization 
 - 再在这个 Orgnization 里面创建一个 Space。这个就是你的书籍项目了。 
 - 然后就可以在线写书了～书籍的在线浏览地址为：

2. 在 gitbhub上发布书籍源码
 - 在GitBook项目目录，如gitbook中，执行如下命令，创建本地git仓库：
 ```js
 git init
 ````
 - 使用文本编辑器，创建名为.gitignore的文件，内容如下：
 ```
 *~
_book
.DS_Store
通过.gitignore文件，本地仓库将忽略临时文件和_book文件夹，达到只保存书籍源码的目的。
 ```
  - 现在可以将本地书籍源码添加到本地git仓库中了：
 ```
 git add .
 ```
 - 添加更新说明
 ```
 	git commit -m '更新说明文字'
 ```
 - 建立本地仓库与远端仓库的对应关系
 ```
 	git remote add origin https://远程仓库地址.git
 ```
 - 将本地仓库内容同步到远端仓库：
 ```
 git push -u origin master
 至此，就完成了将gitbook源码推送到远程仓库的任务，之后书籍内容修改后，执行如下操作即可：
 git add .
 git commit -m '更新说明文字'
 git push -u origin master
 ```
## 在github上发布和管理书籍
需要在原有本地仓库新建一个分支，在这个分支中，只保留_book文件夹中的内容，然后将这些内容推送到远程仓库的pages分支，启用pages服务，最终达到免费发布电子书的目的。
1. 新建分支
```
git checkout -b gh-pages
新建名为pages的分支，分支名称随意，但最好能反映出分支的用途。
```
2. 删除不需要的文件
```
切换到pages分支后，我们需要将_books目录之外的文件都清理掉：
git rm --cached -r .
git clean -df
rm -rf *~
```
3. 添加忽略文件
使用文本编辑器，创建名为.gitignore的文件，内容如下：
```
*~
_book
.DS_Store
通过.gitignore文件，本地仓库将忽略临时文件和_book文件夹。
```
4. 复制_book文件夹到分支根目录
```
cp -r _book/* .
```
5. 添加文件
git add .
6. 添加更新说明
git commit -m '更新说明'
7. 推送
git push -u origin gh-pages
现在开启git托管网站的pages服务即可。
## gitbook 与 github 关联同步
新版 gitbook.com 不支持本地版本管理了，但是对 github 的集成支持的不错。可以通过配置，实现在 github 项目里面提交内容，gitbook 平台会自动同步过去。
- 在 gitbook 平台里，进入要设置的 space，也就是你的书
- 点左下角的配置按钮，进入配置，点击 Intergrations ，找到 github。
- 点击 link you github repository 按钮，根据向导，登录 github ，选择 reposirory，选择分支，完成绑定和同步。(你还可以选择是 gitbook 同步 github ，还是 github 同步 gitbook)
- 需要注意的是：绑定的 github 仓库分支里面要是 gitbook 的源码，也就是那些 md 文件。而不是 build 之后生成的 html 文件。