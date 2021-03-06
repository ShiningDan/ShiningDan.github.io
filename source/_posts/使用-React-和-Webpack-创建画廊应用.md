﻿---
title: 使用 React 和 Webpack 创建画廊应用
date: 2017-02-16 14:12:33
categories: coding
tags:
  - HTML
  - CSS
  - JavaScript
  - React
  - Webpack
---

本文是在学习 React 的时候，自己用来做练习的Demo，在 [React实战--打造画廊应用](http://www.imooc.com/learn/507) 也有一篇使用 React 打造画廊应用的Demo，但是本文没有参考他的实现，有兴趣的同学可以去这个视频学习对比。

本文在前端设计方面，是学习[慕课网 Lyn](http://www.imooc.com/t/104593)的视频。如果在设计方面有问题，建议参考原视频。

项目最终效果：

![](http://ojt6zsxg2.bkt.clouddn.com/974aa23d57a72dd84ec464a88acc6822.png)

项目下载方法：

这个小项目的 Demo 我已经传到网上去了，可以在 github 上进行下载。具体步骤如下：

安装方法是：

```
https://github.com/ShiningDan/react-gallery.git
cd react-gallery/
npm install
npm run build
npm run start
```

就可以在 http://localhost:8080/index.html 上看到项目的展示效果。

<!--more-->

下面介绍如何从零开始完成这个项目。

## 准备工作

### 创建项目

在 Github 上创建一个 Repository，叫 [react-gallery](https://github.com/ShiningDan/react-gallery)，并且使用 Git 在本地创建一个 react-gallery 文件夹。

```
git clone https://github.com/ShiningDan/react-gallery.git
```

上面 git clone 后面的链接为你自己创建好的项目。

### 安装 webpack

进入项目目录：

```
cd react-gallery
npm init
```

在此之前你应该已经安装了 node.js.

```
npm install webpack --save-dev
```

参数 `-g` 表示我们将全局(global)安装 webpack, 这样你就能使用 webpack 命令了.

webpack 也有一个 web 服务器 webpack-dev-server, 我们也安装上

```
npm install webpack-dev-server --save-dev
```

### webpack 配置文件

webpack 使用一个名为 webpack.config.js 的配置文件, 现在在你的项目根目录下创建该文件. 我们假设我们的工程有一个入口文件 `app.js`, 该文件位于 app/ 目录下, 并且希望 webpack 将它打包输出为 build/ 目录下的 `bundle.js` 文件. `webpack.config.js` 配置如下:

```
var path = require("path");

module.exports = {
	entry: path.resolve(__dirname, "app/app.js"),
	output: {
		path: path.resolve(__dirname, "build"),
		filename: "bundle.js"
	}
}
```

**注意，如果文件的路径不是在当前目录下，则需要使用 `path.resolve` 来创建文件路径**

现在让我们测试一下, 创建 `app/app.js`文件, 填入一下内容:

```
document.write("Hello React");
```

创建 index.html, 填入以下内容:

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>React Webpack Gallery</title>
</head>
<body>
	<script src="build/bundle.js"></script>
</body>
</html>
```

其中 script 引入了 `build/bundle.js`, 这是 webpack 打包后的输出文件.

运行 `webpack` 打包, 运行 `webpack-dev-server` 启动服务器. 访问 `http://localhost:8080/index.html`, 如果一切顺利, 你会看到打印出了 Hello React.

### 配置 package.json

在 `package.json`, 修改 `scripts` 的键值如下:

```
"scripts": {
  "start": "webpack-dev-server --progress --colors  --watch",
  "build": "webpack"
}
```

注：`package.json`中的脚本部分已经默认在命令前添加了`node_modules/.bin`路径，所以无论是全局还是局部安装的Webpack，你都不需要写前面那指明详细的 script 中运行命令所对应的路径了

现在执行 `npm run build` 相当于 `webpack`, `npm run start` 相当于 `webpack-dev-server`. 当项目变得相当复杂时, 你可以使用这种技巧隐藏其中的细节.

### 安装依赖

安装 React:

```
npm install react react-dom --save-dev
```

安装 Babel 的 loader 以支持 ES6 语法:

```
npm install babel-core babel-loader babel-preset-es2015 babel-preset-react --save-dev
```

然后配置 `webpack.config.js` 来使用安装的 loader.

```
var path = require("path");

module.exports = {
	entry: path.resolve(__dirname, "app/app.js"),
	output: {
		path: path.resolve(__dirname, "build"),
		filename: "bundle.js"
	},
	module: {
		loaders: [
			{
				test: /\.jsx?$/,
				exclude: /node_modules/,
				loader: "babel-loader",
				query: {
					presets: ["es2015", "react"]
				}
			}
		],
	}
}
```

接下来测试一下开发环境是否搭建完成.

打开 app.js, 修改内容为:

```
import React from "react";
import ReactDOM from "react-dom";

class HelloReact extends React.Component {
	render() {
		return (
			<div>Hello World, Hello React!</div>
		);
	}
}

ReactDOM.render(<HelloReact />,
	document.getElementById("content")
);
```

这里组件 `HelloReact` 被装载到 `id` 为 `content` 的 DOM 元素, 所以相应的需要修改 `index.html` .

```
<body>
	<div id="content"></div>
	<script src="build/bundle.js"></script>
</body>
```

再次打包运行, 访问 `http://localhost:8080/index.html` 如果可以看到打印出了 Hello World 那么开发环境就算搭建完成了.

## 在写项目之前

关于散列画廊的制作方法，可以参考[慕课网 Lyn](http://www.imooc.com/learn/366) 的视频，这里不对实现的方法做过多的讲解。

在开始写第一个组件之前, 让我们分析一下到底我们需要哪些组件.

![](http://ofjjubwp5.bkt.clouddn.com/image/png/img70.PNG)

上图是的最终效果的部分截图, 我们将其分为几个组件, 用不同颜色的线框标出

![](http://ojt6zsxg2.bkt.clouddn.com/image/pngimg701.png)

我们可以看出其中包含以下几个组件.

* GallerryContainer(蓝色)：所有组件的容器
* GalleryPhoto(红色)：照片代表的组件
* GalleryNavbar(最下面)：对应每张照片的导航条外框
* GalleryNavIcon(每一个圆点)：每一个原点对应一张图片

把这些组成为一棵组件树.

* GalleryContainer
    * GalleryPhoto * n
    * GalleryNavbar
        * GalleryIcon * n

### 编写大致的模板

上一节我们知道了整个页面的组件结构, 在这一节我们根据这些结果编写出一个大致的模板. 先在 app 目录下为每个组件建立文件，`GalleryContainer.js GalleryPhoto.js GalleryNavbar.js GalleryIcon.js`

```
cd app
touch GalleryContainer.js GalleryPhoto.js GalleryNavbar.js GalleryIcon.js
```

编辑 `GalleryIcon.js`

```
import React from "react";

export default class GalleryIcon extends React.Component{
	render() {
		return (
			<div>I am GalleryIcon</div>
		);
	}
}
```

就先这样, 具体的实现现在先不去考虑, 记得我们现在只是编写一个大致的结构.

编辑`GalleryNavbar.js`

```
import React from "react";
import GalleryIcon from "./GalleryIcon.js"

export default class GalleryNavbar extends React.Component {
	render() {
		return (
			<div>
				I am GalleryNavbar
				<GalleryIcon />
				<GalleryIcon />
			</div>
		);
	}
}
```

因为 `GalleryNavbar` 是 `GalleryIcon` 的容器，所以需要引入它

编辑`GalleryPhoto.js`

```
import React from "react";

export default class GalleryPhoto extends React.Component {
	render() {
		return (
			<div>I am GalleryPhoto</div>
		);
	}
}
```

编辑`GalleryContainer.js`

因为`GalleryContainer` 是 `GalleryNavbar` 和 `GalleryPhoto` 的容器，所以也需要引入他们。

```
import React from "react";
import GalleryPhoto from "./GalleryPhoto.js";
import GalleryNavbar from "./GalleryNavbar.js"

export default class GalleryContainer extends React.Component {
	render() {
		return (
			<div>
				I am GalleryContainer
				<GalleryPhoto />
				<GalleryPhoto />
				<GalleryNavbar />
			</div>
		);
	}
}
```

最后修改入口文件 `app.js`:

```
import React from "react";
import ReactDOM from "react-dom";
import GalleryContainer from "./GalleryContainer.js";

ReactDOM.render(
	<GalleryContainer />,
	document.getElementById("content")
);
```

这时访问 http://localhost:8080/index.html 可以看到下图的效果

![](http://ojt6zsxg2.bkt.clouddn.com/3e5faac3197dd50dfe70ff314c31e4d6.png)

说明几个组件的创建都成功了，下面我们开始分别写各个组件。

### 编写 GalleryPhoto

整个 GalleryPhoto 包含了正面和背面，我们先从正面来写：

#### 照片正面效果

正面的效果如下：

![](http://ojt6zsxg2.bkt.clouddn.com/acc3a77537e172ed14e5ea47eeec402c.png)

重新编辑 `GalleryPhoto.js` 的代码:

首先在 `GalleryPhoto.js`里添加 `getFront()` 函数，返回正面的 div。

```
getFront() {
		return (
			<div className="side-front">
				<img src={photoImage} alt=""/>
				<p>第一张图片的描述</p>
			</div>
		);
	}
```


在前面几节的开发中, 还记得你是怎么引入其他的 js 文件的吗? import. 实际上这是 ES6 的模块系统, 这里的 js 文件作为模块被其他模块引入. 但除了 js 文件, 在开发时我们还会涉及其他的资源文件, 如图像, 字体, 样式等, 它们也需要被模块化. 在这里, 如果 Logo 图片也能被模块化然后引入该多好. 我们需要再次配置 Webpack.

安装对应的 loader:

```
npm install url-loader file-loader --save-dev
```

配置 `webpack.config.js`

```
//...
 loaders: [
		{
			test: /\.jsx?$/,
			exclude: /node_modules/,
			loader: "babel-loader",
			query: {
				presets: ["es2015", "react"]
			}
		},
		{
			test: /\.(png|jpg|gif)$/,
			loader: "url-loader?limit=8192" // 这里的 limit=8192 表示用 base64 编码 <= ８K 的图像
		},
		]
//...
```

这时使用 webpack 就可以将图像作为正确的模块导入了。

```
import React from "react";
import photoImage from "./image/1.jpg";

export default class GalleryPhoto extends React.Component {
	getFront() {
		return (
			<div className="side-front">
				<img src={photoImage} alt=""/>
				<p>第一张图片的描述</p>
			</div>
		);
	}

	render() {
		return (
			<div className="photo">
				{this.getFront()}
			</div>
		);
	}
}
```

最后我们需要添加样式, 还是回到刚刚的问题, 怎么引入样式?

我们也需要将样式模块化.

安装相应的 loader:

```
npm install css-loader style-loader --save-dev
```
`css-loader` 处理 css 文件中的 url() 表达式.

`style-loader` 将 css 代码插入页面中的 style 标签中.

在 `webpack.config.js` 中配置新的 loader.

```
{
	 test: /\.css$/,
	 loader: 'style-loader!css-loader'
},
```

新建一个 css 文件`app/style/GalleryPhoto.css`

```
.photo{width: 160px;height: 190px;position: absolute;box-shadow: 0 0 1px rgba(0, 0, 0, 0.01);transition: all 0.5s;}
.photo .side-front{padding: 10px;position: absolute;padding-bottom: 0px;background-color: #ddd;}
.photo .side-front img{width: 138px;height: 148px;display: block;margin: 0 auto;border: 1px solid #aaa;}
.photo .side-front p{display: block;height: 30px;line-height: 30px;text-align: center;color: #333;font-size: 12px;}

```

然后在 `GalleryPhoto.js` 中引用它：

```
import "./style/GalleryPhoto.css";
```

再建立一个全局的 css 文件 `app.css`

```
*{padding: 0; margin: 0;font-size: 14px;}
```

然后在 `app.js` 中引入

```
import "./style/app.css";
```

打包运行看看吧.

#### 照片背面效果

重新编辑 `GalleryPhoto.js` 的代码:

在 `GalleryPhoto.js`里添加 `getBack()` 函数，返回背面的 div。

```
getBack() {
		return (
			<div className="side-back">
				<p>这是背面的描述，这是背面的描述，这是背面的描述，这是背面的描述，这是背面的描述，这是背面的描述，这是背面的描述，
				</p>
			</div>
		);
	}
```

然后调用 `getBack()` 函数：

```
<div className="photo">
				{this.getFront()}
				{this.getBack()}
			</div>

```

为 `.side-back` 添加样式:

```
.photo .side-back{padding: 10px;position: absolute;width: 140px;height: 180px;overflow: hidden;background-color: #ddd;padding-bottom: 0px;}
```

可以打包运行看一看 `.side-back` 的结果。

#### 实现点击翻面效果

点击翻面效果的实现，其实就是 `.side-front` 和 `.side-back` 显示的交换.

为了方便实现照片的翻转，使用`.photo-wrap`包裹照片的正反两面。

```
getPhotoWrap() {
		return (
			<div className="photo-wrap">
				{this.getFront()}
				{this.getBack()}
			</div>
		);
	}
```

然后对 `.photo-wrap` 添加 CSS 样式，并且将 `.side-front` 放在正面，`.side-back` 放在背面：

```
.photo-wrap{-webkit-transform-style: preserve-3d;-webkit-backface-visibility: hidden;width: 100%;height: 100%;transition: all 0.6s;border: 1px solid #aaa;cursor: pointer;}
.photo-wrap .side-front{-webkit-transform: rotateY(0deg);}
.photo-wrap .side-back{-webkit-transform: rotateY(180deg);}
```

下面我们要做的是，如果点击 `.photo-wrap`，就将图片旋转 180 度.

我们将使用两个 class 来决定图片是正面朝上还是反面朝上。

`photo-f` 代表当前图片正面朝上，`.photo-b`代表当前图片反面朝上，并且在点击 `.photo-wrap` 的时候触发这两个 Class 之间的修改。

首先添加 state 代表这两个 class

```
constructor(props) {
		super(props);
		this.state = {
			photoFB: "photo-f",
		};
	}
```

注意：ES6 中不适用 getInitialState 来设置 state，而是在 constructor 中设置 state。

然后添加 `{photoFB}` 到 `className` 里面，并且添加 `onClick` 事件。

```
handleClick(event) {
		if (this.state.photoFB === "photo-f") {
			this.setState({
				photoFB: "photo-b",
			})
		}
		else
			this.setState({
				photoFB: "photo-f",
			});
	}
	getPhotoWrap() {
		return (
			<div className={"photo-wrap " + this.state.photoFB} onClick={this.handleClick.bind(this)}>
				{this.getFront()}
				{this.getBack()}
			</div>
		);
	}
```

最后添加对应`.photo-f`和 `.photo-b` 的 css 样式。

```
.photo-f.photo-wrap{transform: rotateY(0deg);}
.photo-b.photo-wrap{transform: rotateY(180deg);}
```

**注意，使用 `transform-style: preserve-3d;backface-visibility:hidden;` 等属性有可能会在不同的浏览器中导致图像闪烁无法旋转等情况出现。**

所以最后迫于无奈，只能用 `display:none` 来控制背面的显示，并且将`transform-style: preserve-3d;backface-visibility:hidden;`注释掉，以后如果没有闪烁的 bug，就可以将其反注释，并删除 `display:none`。

此时的CSS 样式为：

```
.photo{width: 160px;height: 190px;position: absolute;box-shadow: 0 0 1px rgba(0, 0, 0, 0.01);transition: all 0.5s;}
.photo .side-front{padding: 10px;position: absolute;padding-bottom: 0px;background-color: #ddd;}
.photo .side-front img{width: 138px;height: 148px;display: block;margin: 0 auto;border: 1px solid #aaa;}
.photo .side-front p{display: block;height: 30px;line-height: 30px;text-align: center;color: #333;font-size: 12px;}
.photo .side-back{padding: 10px;position: absolute;width: 140px;height: 180px;overflow: hidden;background-color: #ddd;padding-bottom: 0px;}
.photo-wrap{/*transform-style: preserve-3d; backface-visibility:hidden;*/width: 100%;height: 100%;transition: all 0.6s;border: 1px solid #aaa;cursor: pointer;}
.photo-wrap .side-front{transform: rotateY(0deg);}
.photo-wrap .side-back{transform: rotateY(180deg);}
.photo-f.photo-wrap{transform: rotateY(0deg);}
.photo-b.photo-wrap{transform: rotateY(180deg);}
.photo-f.photo-wrap .side-back{display: none;}
.photo-f.photo-wrap .side-front{display: block;}
.photo-b.photo-wrap .side-front{display: none;}
.photo-b.photo-wrap .side-back{display: block;}
```

### 编写 GalleryContainer

修改 `GalleryContainer.js`，返回 `div#container`

```
render() {
		return (
            <div id="container">
				<GalleryPhoto />
			</div>
		);
	}
```

并且创建 `GalleryContianer.css`

```
#container{width: 800px;height: 400px;margin: 100px auto;border: 1px solid rebeccapurple;overflow: hidden; perspective: 800px;-webkit-perspective:800px;background-color: #666}
```

在 `GalleryContainer.js` 导入 css 文件

```
import "./style/GalleryContainer.css";
```

#### 批量加载 GalleryPhoto

首先在 `GalleryContainer.js` 中将图片以模块的形式导入。

```
const requireContext = require.context("./image", true, /^\.\/.*\.jpg$/);
const images = requireContext.keys().map(requireContext);
```

这时 `images` 就是一个数组，包括了所有的图片。

使用 `images` 生成 `photos`，其中包含了所有图片的链接以及描述信息，然后调用 `GalleryPhoto` 组件。

```
getPhotos() {
		let photos = []
		images.forEach( function(image, index) {
			photos[index] = {
				img: images[index],
				title: "照片"+index,
				desc: ("照片"+index+"的描述").repeat(5),
			};
		});

        return (
        	<div className="photos">
        	{
        		photos.map(function(photo, index) {
        			return (
        				<GalleryPhoto key={"photo-"+index} id={"photo-"+index} imgSrc={photo.img} imgTitle={photo.title} imgDesc={photo.desc}/>
        			);
        		})
        	}
           	</div>
        );
	}
```

修改 `GalleryContainer.js` 的 `render` 函数，调用`getPhotos` 方法。

```
render() {
		return (
			<div id="container">
				{this.getPhotos()}
			</div>
		);
	}
```

此时，我们要修改 `GalleryPhoto` 组件，接收 `GalleryContainer` 传来的参数。

```
export default class GalleryPhoto extends React.Component {
	constructor(props) {
		super(props);
		this.state = {
			photoFB: "photo-f",
		};
	}
	getFront(src, title) {
		return (
			<div className="side-front">
				<img src={src} alt=""/>
				<p>{title}</p>
			</div>
		);
	}

	getBack(desc) {
		return (
			<div className="side-back">
				<p>{desc}</p>
			</div>
		);
	}
	handleClick(event) {
		if (this.state.photoFB === "photo-f") {
			this.setState({
				photoFB: "photo-b",
			})
		}
		else
			this.setState({
				photoFB: "photo-f",
			});
	}
	getPhotoWrap(src, title, desc) {
		return (
			<div className={"photo-wrap " + this.state.photoFB} onClick={this.handleClick.bind(this)}>
				{this.getFront(src, title)}
				{this.getBack(desc)}
			</div>
		);
	}

	render() {
		return (
			<div className="photo" id={this.props.id}>
				{this.getPhotoWrap(this.props.imgSrc, this.props.imgTitle, this.props.imgDesc)}
			</div>
		);
	}
}
```

完成后打包运行，我们可以在浏览器调试窗口看到 15（因为我有是15张照片） 个`GalleryPhoto` 组件生成的实例。

![](http://ojt6zsxg2.bkt.clouddn.com/eaeb1125feb0d6d36592fc95cae4f623.png)

![](http://ojt6zsxg2.bkt.clouddn.com/510348f5e63b09e4e0610fb30c9fe2ca.png)

但是此时所有的照片都是重叠在一起的，我们需要将照片分布到整个 `#container` 里面。

#### 设置照片居中

在我们的显示效果中，有一张照片要分布在 `#container` 的正中央，然后其他的照片在两边随机分布，我们先在`GalleryPhoto` 中添加 `.photo-center` 样式。

```
.photo-center{top: 50%; left: 50%;margin: -80px 0 0 -95px;-webkit-transform: rotateY(0deg);z-index: 1;}
```

然后设置一个 state 和 `.photo-center` 对应：

```
this.state = {
			photoFB: " photo-f",
			photoCenter: "",
		};

```

同时暴露两个对外的函数，允许父组件调用修改该组件的 `photoCenter`：

```
setCenter() {
	this.setState({
		photoCenter: " photo-center",
	});
}
removeCenter() {
	this.setState({
		photoCenter: "",
	});
}
```

在 `GalleryContainer` 中，我们需要对生成的 `GalleryPhoto` 进行居中的功能，为了能够找到所有的 `GalleryPhoto`，修改创建 `GalleryPhoto` 的代码，为每个 `GalleryPhoto` 添加一个 `ref`。

```
getPhotos() {
	let photos = []
	images.forEach( function(image, index) {
		photos[index] = {
			img: images[index],
			title: "照片"+index,
			desc: ("照片"+index+"的描述").repeat(5),
		};
	});

    return (
    	<div className="photos">
    	{
    		photos.map(function(photo, index) {
    			return (
    				<GalleryPhoto key={"photo-"+index} ref={"photo-"+index} imgSrc={photo.img} imgTitle={photo.title} imgDesc={photo.desc}/>
    			);
    		})
    	}
       	</div>
    );
}
```

通过 `ref={"photo-"+index}`，将不同的 `GalleryPhoto` 的 `ref` 分别设置成：`photo-0、photo-1...photo-14`

最后创建 `setCenter(index)` 函数，通过调用该函数，来调用 `GalleryPhoto` 的 `setCenter` 和 `removeCenter` 方法，实现子组件的居中功能。

```
setCenter(index){
	for (let i = 0; i <  images.length; i++) {
		this.refs["photo-"+i].removeCenter()
	}
	this.refs["photo-"+index].setCenter();
}
```

好啦！

让我们来测试一下 `setCenter` 方法吧。

为了确保在调用 `setCenter` 方法的时候，所有的`GalleryPhoto`子组件都已经生成，我们需要在 `componentDidMount` 中调用该方法。在 `GalleyContainer` 中添加 `componentDidMount` 方法如下，设置 `photo-2` 图片居中。 

```
componentDidMount() {
	this.setCenter(2);
}
```

好了，现在打包运行试一试吧。

![](http://ojt6zsxg2.bkt.clouddn.com/d0cfeacaa84e4697630d76d91571d697.png)

运行的结果如上图，我们可以看到，`photo-2` 的照片被取出居中了。这一部分功能完成。


#### 照片随机分布

当设置好照片居中以后，我们要设置其他的照片在居中照片两侧随机分布。虽然是随机分布，但是照片的位置还是有一定范围的。这个范围的计算可以参考 Lyn 老师的视频。

首先设置照片在 `#container` 中分布的范围。

在不使用 React 的时候，是通过 `range` 函数获取 `#container` 和 `.photo` 的宽度和高度，然后计算得到，计算方法如下面函数：

```
range() {
        let range = { left:{x:[], y:[]}, right:{x:[], y:[]}};

        let wrap = {
            width:document.getElementById("container").clientWidth,
            height:document.getElementById("container").clientHeight
        }; 
        let photo = {
            width:document.getElementsByClassName("photo")[0].clientWidth,
            height:document.getElementsByClassName("photo")[0].clientHeight
        };

        range.left.x.push(0-photo.width/2);
        range.left.x.push(wrap.width/2-photo.width);
        range.left.y.push(0-photo.height/2);
        range.left.y.push(wrap.height-photo.height/2);

        range.right.x.push(wrap.width/2+photo.width/2);
        range.right.x.push(wrap.width-photo.width/2);
        range.right.y.push(0-photo.height/2);
        range.right.y.push(wrap.height-photo.height/2);
        this.setState({
            range: range,
        });
    }
```

在 `componentDidMount` 里面添加该函数。

为什么要在 `componentDidMount` 里添加该函数呢？因为该函数要调用 `#container` 还有 `.photo` 等元素，但是这些元素只有在渲染之后才会出现。所以在 `componentDidMount` 中调用该函数可以确保查找这些元素的时候元素已经存在。

并且初始化 `this.state.range`

```
constructor(props) {
		super(props);
		this.state = {
			range: {},
		};
	}

```

但是这里出现了一个问题，我目前还不知道是什么原因。问题如下：

```
componentDidMount() {
	range()
	console.log(this.state.range)
	//this.setCenter(2);
}
```

当我调用 `range()` 后输出 `this.state.range`，结果并没有获得计算好的 `range`，输出的结果是 `{}`，说明计算并没有立刻进行。如果不是立刻进行范围的计算，在别的地方调用 `range` 的时候就会报错，这不是我想要的。所以，我直接计算好以后初始化 `this.state.range`：

```
constructor(props) {
	super(props);
	this.state = {
		range: {
			left: {
				x: [-80, 240],
				y: [-95, 305],
			},
			right: {
				x: [480, 720],
				y: [-95, 305],
			}
		}
	};
}
```

设置完随机照片的位置范围以后，我们下面要做的，就是决定哪些照片要放在居中照片的左侧，哪些要放在右侧，并且每一张照片都有几率左右倾斜。

```
randomInt(min, max){
    let diff = max-min+1;
    return Math.ceil(Math.random()*diff + min - 1);
}

randomArray(arr){
    let rArr = [];
    do{
        let index = this.randomInt(0, arr.length-1);
        rArr.push(arr.splice(index,1).pop());
    }while(arr.length>0)
    return rArr;
}

setLeftRightRoll() {
	let photos = [];
	for (let i = 0; i < images.length; i++) {
		photos.push(this.refs["photo-"+i]);
	}
	photos = this.randomArray(photos);
	let photoLeft = photos.splice(Math.ceil(photos.length/2), Math.ceil(photos.length/2));
    let photoRight = photos;
    for (let i = 0; i < photoLeft.length; i++) {
    	let style = {
    		left: this.randomInt(this.state.range.left.x[0], this.state.range.left.x[1]),
    		top: this.randomInt(this.state.range.left.y[0], this.state.range.left.y[1]),
    		transform: 'rotate('+this.randomInt(-60, 60) + 'deg)',
    	};
    	photoLeft[i].setLeftRightRoll(style);
    }
    for (let i = 0; i < photoRight.length; i++) {
    	let style = {
    		left: this.randomInt(this.state.range.right.x[0], this.state.range.right.x[1]),
    		top: this.randomInt(this.state.range.right.y[0], this.state.range.right.y[1]),
    		transform: 'rotate('+this.randomInt(-60, 60) + 'deg)',
    	};
    	photoRight[i].setLeftRightRoll(style);
    }
}
```

这个方法实现的功能有：

1. randomInt(min, max)：生成一个介于 min 和 max 之间的整数值
2. randomArray(arr)：接收一个数组，并且将该数组的元素随机排序后返回
3. setLeftRigthRoll()：将所有的子组件随机分布在 `#container` 的左右两侧，并且在 -60度到 60度之间随机旋转一个角度。

`GalleryContainer` 会调用 `GalleryPhoto` 子组件的 `setLeftRightRoll()` 方法，并且将生成的 css 样式传给他，所以我们要在 `GalleryPhoto` 中创建这个方法：

首先我们添加一个名为 `photoStyle` 的 state

```
constructor(props) {
	super(props);
	this.state = {
		photoFB: "photo-f",
		photoCenter: "",
		photoStyle: {},
	};
}
```

这个 state 代表着 `GallryPhoto` 的样式，将该样式添加到 `GallryPhoto` 上：

```
render() {
	return (
		<div className={"photo" + this.state.photoCenter} style={this.state.photoStyle}>
			{this.getPhotoWrap(this.props.imgSrc, this.props.imgTitle, this.props.imgDesc)}
		</div>
	);
}
```

然后通过 `setLeftRightRoll()` 函数来设置 `photpStyle` 的样式：

```
setLeftRightRoll(style) {
	this.setState({
		photoFB: "photo-f",
		photoCenter: "",
		photoStyle: style,
	})
}
```

这时我们就可以在 `GalleryContainer.componentDidMount` 函数中调用写好的函数了：

```
componentDidMount() {
	this.setLeftRightRoll();
	this.setCenter(2);
}
```

打包运行看一看：

![](http://ojt6zsxg2.bkt.clouddn.com/ea1541d4daa146aebeb504c1e032c8b9.png)

左右两边的图片到是分布好了，但是中间的图片怎么不见了呢？

原来是 `setLeftRightRoll()` 中设置的样式是直接设置到元素上的，而 `.photo-center` 中设置元素居中的样式是通过 class 引入的，其优先级没有直接在元素上直接设置样式的优先级高，所以我们需要在 `GalleryContainer.setCenter` 中重置居中元素的样式。

```
setCenter(index){
	for (let i = 0; i <  images.length; i++) {
		this.refs["photo-"+i].removeCenter()
	}
	let style = {
		left: "",
		top: "",
		transform: "rotateY(0deg)",
	};
	this.refs["photo-"+index].setCenter(style);
}
```

并且修改 `GalleryPhoto.setCenter` 方法，接收 style：

```
setCenter(style) {
	this.setState({
		photoFB: "photo-f",
		photoCenter: " photo-center",
		photoStyle: style,
	});
}
```

打包运行试试吧。

### 编写Navbar

#### 编写 GalleryIcon

```
render() {
	return (
		<i className="nav-i"></i>
	);
}
```

添加对应的样式：

```
.nav-i{display: inline-block;background-color: #333;width: 26px;height: 26px;border-radius: 13px;margin:0 10px;cursor: pointer;transform: scale(0.5);}
```

#### 编写 GallryNavBar

```
render() {
	let icons = [];
	for (let i = 0; i < this.props.navLength; i++) {
		icons.push(< GalleryIcon key={"nav-"+i}/>);
	}
	return (
		<div className="nav">{icons}</div>		
	);
}
```

添加对应的样式：

```
.nav{width: 100%;height: 26px;line-height: 26px;position: absolute; bottom: 36px;text-align: center;}
```

在 `GalleryContainer` 中创建 `GallryNavbar`，并且在 `GalleryNavbar` 中创建 `GalleryIcon`

```
getNavbar() {
	return (
		<GalleryNavbar navLength={images.length} />
	);
}
render() {
	return (
		<div id="container">
			{this.getPhotos()}
			{this.getNavbar()}
		</div>
	);
}
```

打包并运行

### 为 GalleryIcon 添加点击动画

为 `GalleryIcon` 添加的动画有，当点击某一个导航点时，会把该导航点增大，并且将该点对应的 `GallertPhoto` 居中。

#### 增大效果

增大效果，通过设置一个 `.nav-current` 的 css 样式，并且将该样式赋值给目前点击的导航点 className 即可。

#### 设置居中

设置居中的方法，可以在 `GalleryContainer` 中将 `setCenter` 等方法的引用传给 `GalleryIcon`，并且将该方法添加到 `GalleryIcon`  的 `onClick` 事件中。

修改的代码如下：

`GalleryIcon.css`

```
.nav-current{transform: scale(0.8);}
```

`GalleryIcon.js`

```
constructor(props) {
	super(props);
	this.state = {
		navCurrent: "",
	}
}

setCurrent() {
	this.setState({
		navCurrent: "nav-current",
	});
}

removeCurrent() {
	this.setState({
		navCurrent: "",
	});
}

handleClick(event) {
	let index = this.props.id.slice(4);
	this.props.handleNavIconClick(index);
}

render() {
	return (
		<i className={"nav-i " + this.state.navCurrent} onClick={this.handleClick.bind(this)}></i>
	);
}
```

`GalleryNavbar.js`

```
render() {
	let icons = [];
	for (let i = 0; i < this.props.navLength; i++) {
		icons.push(< GalleryIcon key={"nav-"+i} id={"nav-"+i} ref={"nav-"+i} handleNavIconClick={this.props.handleNavIconClick}/>);
	}
	return (
		<div className="nav">{icons}</div>		
	);
}
```

`GalleryContainer.js`

```
handleNavIconClick(index) {
	this.setLeftRightRoll();
	this.setCenter(index);
	for (let i = 0; i < images.length; i++) {
		this.refs["navbar"].refs["nav-"+i].removeCurrent();
	}
	this.refs["navbar"].refs["nav-"+index].setCurrent();
}
```

打包运行，就可以看到效果啦！

### 设置照片点击居中

现在在展示页面，可以实现点击居中的照片实现翻转，也可以点击两侧的照片实现翻转，但是这个逻辑和我们需要的不一样。我们需要的是点击居中的照片实现翻转，点击两侧的照片，则被点击的照片会被居中，为了实现上述功能，我们需要在 `GalleryPhoto` 中修改 `handleClick` 的逻辑：

```
handleClick(event) {
	if (this.state.photoCenter !== " photo-center") {
		let index = this.props.id.slice(6);
		this.props.handlePhotoClick(index);
	} else {
		if (this.state.photoFB === "photo-f") {
			this.setState({
				photoFB: "photo-b",
			})
		}
		else {
			this.setState({
				photoFB: "photo-f",
			});
		}
	}
}
```

在创建 `GalleryPhoto` 的时候修改`getPhotos` 方法，为其指定 `id`：

并且通过 `props` 将 `handleNavIconClick` 方法暴露给 `GalleryPhoto` 组件，在点击组件的时候达到和点击 `GalleryIcon` 一样的效果。

```
photos.map(function(photo, index) {
    			return (
    				<GalleryPhoto key={"photo-"+index} id={"photo-"+index} handlePhotoClick={this.handleNavIconClick.bind(this)} ref={"photo-"+index} imgSrc={photo.img} imgTitle={photo.title} imgDesc={photo.desc}/>
    			);
    		}.bind(this))
```

完成修改，现在可以打包运行啦。


































