# a_simplefilm

运行vue项目的环境配置

- node.js环境（npm包管理器）
- cnpm  npm的淘宝镜像 【可选】

1、安装去node.js官网下载 node.js，点击运行安装一路next。

2、用node.js自带的包管理器 npm 安装中国镜像，可以加速项目依赖包的下载 npm install -g cnpm --registry=http://registry.npm.taobao.org 【可选】

3、打开cmd，进入项目工作目录，比如 cd E:\Github\a_simplefilm，输入 (c)npm install ，等下载完依赖可以发现目录下多了一个node_modues包。继续输入 npm run dev，如果8080端口没有被占用，浏览器输入 localhost:8080 



## 分页概要

使用element-ui评分组件 + 自渲染评分

<img src=".\imgs\img1.PNG">



## 电影名搜索

包含别名，输入关键字，**按回车或者点击搜索按钮**，即可查找，分页组件根据返回结果数实时变化，类别标签跳至所有。若搜索输入为空，默认页面重置数据，显示所有类别第一页。

<img src=".\imgs\img2.png">



<img src=".\imgs\img3.png">

## 电影详情

点击imdb可跳转前往。点击返回，前一页面数据状态不变

<img src=".\imgs\img4.png">







## 电影类别

页面创建时，按照各类别逆序渲染生成标签页栏，切换后分页组件实时变化。

<img src=".\imgs\img5.PNG">







## Reference

https://blog.csdn.net/z_xuewen/article/details/85264653 回车搜索

https://www.jianshu.com/p/d1ccef6d8c58 返回保持页面状态