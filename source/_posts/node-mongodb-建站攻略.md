﻿---
title: node+mongodb 建站攻略
date: 2017-03-20 21:35:20
categories: coding
tags:
  - Node.js
  - Express
  - Mongodb
  - Jade
  - Grunt
---

本笔记是根据 [node+mongodb 建站攻略](http://www.imooc.com/learn/75) 教程所记录的笔记。如有需要，可以参考原视频。

## 项目前期准备

后端使用的是 node.js + express。模板引擎是 jade，对时间和日期的格式化使用的是 moment.js

前端使用的是 jQuery 和 Bootstrap。

本地环境使用的是 less + cssmin + jsHint + UglifyJS + mocha + grunt

[express](http://www.expressjs.com.cn/)


开发的流程为：

![](http://ojt6zsxg2.bkt.clouddn.com/ee3c9abb0323bdd59b1474c306fa2da2.png)

<!--more-->

## 项目前后端流程的打通

### 项目结构的初始化

```
npm install express --save
npm install jade --save
npm install mongoose --save
npm install bower -g --save
bower install boostrap
```

### 入口文件编码

app.js:

```
let express = require('express');

let app = express();

app.set('view engine', 'jade');
app.set('port', 3000);

app.get('/', function(req, res) {
    res.render('index', {title: 'imooc'});
})
```

index.jade:

```
<!DOCTYPE html>
html
    head
    body
        title #{title}
```

项目的结构为：

![](http://ojt6zsxg2.bkt.clouddn.com/4da689f7513ed364d721dbf91d5518e7.png)

### 创建四个 jade 视图以及入口文件处理

入口文件如下：

app.js
```
let express = require('express');

let port = process.env.PORT || 3000;
let app = express();

app.set('views', './views');  // 应用的视图目录
app.set('view engine', 'jade'); // 应用的视图引擎
console.log('listen to port', port);
app.listen(port);


app.get('/', function(req, res) {
    res.render('index', {
        title: 'shiningdan 首页'
    });
});

app.get('/admin/list', function(req, res) {  //访问 /admin/list 返回 list.jade 渲染后的效果
    res.render('list', {        // list 是从 views 里面找到的 list.jade
        title: 'shiningdan 列表页'
    })
})

app.get('/admin/movie', function(req, res) {
    res.render('admin', {
        title: 'shiningdan 后台录入页'
    })
})

app.get('/admin/:id', function(req, res) {   // 访问 /admin/3 返回 detail.jade 渲染后的效果
    res.render('detail', {
        title: 'shiningdan 详情页'
    })
})
```

模板文件如下：

```
<!DOCTYPE html>
html(lang="en")
head
    meta(charset="UTF-8")
    meta(name="viewport", content="width=device-width, initial-scale=1.0")
    meta(http-equiv="X-UA-Compatible", content="ie=edge")
    title #{title}
body
    h1 #{title}
```

当访问 http://127.0.0.1:3000/admin/list 等 url 的时候，会找到 list.jade，渲染模板并且返回 html 文件。

### 伪造模板数据跑通前后端交互流程

在 app.js 中需要获取静态资源，新版express4中，要独立安装`static`，`npm install serve-static --save`

在app.js中，

```
var serveStatic = require('serve-static')

app.use(serveStatic('bower_components')
```

bodyParser 已经不再与Express捆绑，需要独立安装。

命令行执行：`npm install body-parser --save`

程序中修改：

```
var bodyParser = require('body-parser')

app.use(bodyParser.urlencoded())
```

最终的项目目录如下：

![](http://ojt6zsxg2.bkt.clouddn.com/c865bfd5e8457711deba5c25763eff33.png)

其中，每一部分的内容为：

app.js

```
let express = require('express');
let path = require('path');
let serveStatic = require('serve-static');
let bodyPaerser = require('body-parser');

let port = process.env.PORT || 3000;
let app = express();

app.set('views', './views/pages/');  // 应用的视图目录
app.set('view engine', 'jade'); // 应用的视图引擎
app.use(serveStatic('bower_components'));
app.use(bodyPaerser.urlencoded({extended: true}));
console.log('listen to port', port);
app.listen(port);


app.get('/', function(req, res) {
    res.render('index', {
        title: 'shiningdan 首页',
        movies: [
            {
                title: '美女与野兽',
                _id: 1,
                poster: 'https://img3.doubanio.com/view/movie_poster_cover/lpst/public/p2417948644.webp'
            },
            {
                title: '美女与野兽',
                _id: 2,
                poster: 'https://img3.doubanio.com/view/movie_poster_cover/lpst/public/p2417948644.webp'
            },
            {
                title: '美女与野兽',
                _id: 3,
                poster: 'https://img3.doubanio.com/view/movie_poster_cover/lpst/public/p2417948644.webp'
            },
            {
                title: '美女与野兽',
                _id: 4,
                poster: 'https://img3.doubanio.com/view/movie_poster_cover/lpst/public/p2417948644.webp'
            },
            {
                title: '美女与野兽',
                _id: 5,
                poster: 'https://img3.doubanio.com/view/movie_poster_cover/lpst/public/p2417948644.webp'
            },
            {
                title: '美女与野兽',
                _id: 6,
                poster: 'https://img3.doubanio.com/view/movie_poster_cover/lpst/public/p2417948644.webp'
            },
        ],
    });
});

app.get('/movie/:id', function(req, res) {   // 访问 /admin/3 返回 detail.jade 渲染后的效果
    res.render('detail', {
        title: 'shiningdan 详情页',
        movie: {
            title: '美女与野兽',
            doctor: '比尔·康顿',
            country: ' 美国',
            language: '英语',
            year: '2017',
            flash: 'https://movie.douban.com/trailer/211279/#content/swf/movie_player_1.4.4.swf',
            poster: 'https://img3.doubanio.com/view/movie_poster_cover/lpst/public/p2417948644.jpg',
            summary: '《美女与野兽》根据迪士尼1991年经典动画片及闻名全球的经典童话改编，讲述了少女贝儿的奇幻旅程——为了解救触怒野兽的父亲，勇敢善良的她只身一人来到古堡，代替父亲被囚禁其中。贝儿克服了恐惧，和城堡里的魔法家具们成为了朋友，也渐渐发现野兽其实是受了诅咒的王子，他可怖的外表下藏着一颗善良温柔的内心；这个故事也带领观众明白——美不仅仅是外表，更重要的是内心。',
        }
    })
})


app.get('/admin/movie', function(req, res) {
    res.render('admin', {
        title: 'shiningdan 后台录入页',
        movie: {
            title: '',
            doctor: '',
            country: '',
            language: '',
            year: '',
            flash: '',
            poster: '',
            summary: '',
        }
    })
})

app.get('/admin/list', function(req, res) {  //访问 /admin/list 返回 list.jade 渲染后的效果
    res.render('list', {        // list 是从 views 里面找到的 list.jade
        title: 'shiningdan 列表页',
        movies: [{
            title: '美女与野兽',
            _id: 1,
            doctor: '比尔·康顿',
            country: ' 美国',
            lanuage: '英语',
            year: '2017',
            flash: 'https://movie.douban.com/trailer/211279/#content/swf/movie_player_1.4.4.swf',
            poster: 'https://img3.doubanio.com/view/movie_poster_cover/lpst/public/p2417948644.jpg',
            summary: '《美女与野兽》根据迪士尼1991年经典动画片及闻名全球的经典童话改编，讲述了少女贝儿的奇幻旅程——为了解救触怒野兽的父亲，勇敢善良的她只身一人来到古堡，代替父亲被囚禁其中。贝儿克服了恐惧，和城堡里的魔法家具们成为了朋友，也渐渐发现野兽其实是受了诅咒的王子，他可怖的外表下藏着一颗善良温柔的内心；这个故事也带领观众明白——美不仅仅是外表，更重要的是内心。',
        }]
    })
})
```

head.jade

```
link(href='/bootstrap/dist/css/bootstrap.min.css', rel='stylesheet', type='text/css')
script(src='/jquery/dist/jquery.min.js')
script(src='/bootstrap/dist/js/bootstrap.min.js')
```

header.jade

```
.container
    .row
        .page-header
            h1 #{title}
            small 重度科幻迷
```

layout.jade

```
<!DOCTYPE html>
html(lang="en")
head
    meta(charset="UTF-8")
    meta(name="viewport", content="width=device-width, initial-scale=1.0")
    meta(http-equiv="X-UA-Compatible", content="ie=edge")
    title #{title}
    include ./includes/head
body
    include ./includes/header
    block content
```

admin.jade

```
extends ../layout

block content
    .container
        .row
            form.form-horizontal(method='post', action='/admin/movie')
                .from-group
                    label.col-sm-2.control-label(for='inputTitle') 电影名字
                    .col-sm-10
                        input#inputTitle.form-control(type='text', name='movie[title]', value='#{movie.title}')
                .from-group
                    label.col-sm-2.control-label(for='inputDoctor') 电影导演
                    .col-sm-10
                        input#inputDoctor.form-control(type='text', name='movie[doctor]', value='#{movie.doctor}')
                .from-group
                    label.col-sm-2.control-label(for='inputCountry') 国家
                    .col-sm-10
                        input#inputCountry.form-control(type='text', name='movie[country]', value='#{movie.country}')
                .from-group
                    label.col-sm-2.control-label(for='inputLanguage') 语种
                    .col-sm-10
                        input#inputLanguage.form-control(type='text', name='movie[language]', value='#{movie.language}')
                .from-group
                    label.col-sm-2.control-label(for='inputPoster') 海报地址
                    .col-sm-10
                        input#inputPoster.form-control(type='text', name='movie[poster]', value='#{movie.poster}')
                .from-group
                    label.col-sm-2.control-label(for='inputYear') 年份
                    .col-sm-10
                        input#inputYear.form-control(type='text', name='movie[year]', value='#{movie.year}')
                .from-group
                    label.col-sm-2.control-label(for='inputFlash') Flash
                    .col-sm-10
                        input#inputFlash.form-control(type='text', name='movie[flash]', value='#{movie.flash}')
                .from-group
                    label.col-sm-2.control-label(for='inputSummary') 简介
                    .col-sm-10
                        input#inputSummary.form-control(type='text', name='movie[summary]', value='#{movie.summary}')
                .form-group
                    .col-sm-offset-2.col-sm-10
                    button.btn.btn-default(type='submit') 录入
```

detail.jade

```
extends ../layout

block content
    .container
        .row
            .col-md-7
                embed(src='#{movie.flash}', allowFullScreen='true', quality='high', width='720', height='600', align='middle', type='application/x-shockwave-flash')
            .col-md-5
                dl.dl-horizontal
                    dt 电影名字
                    dd #{movie.title}
                    dt 导演
                    dd #{movie.doctor}
                    dt 国家
                    dd #{movie.country}
                    dt 语言
                    dd #{movie.language}
                    dt 上映年份
                    dd #{movie.year}
                    dt 简介
                    dd #{movie.summary}
```

index.jade

```
extends ../layout

block content
    .container
        .row
            each item in movies
                .col-md-2
                    .thumbnail
                        a(href='/movie/#{item._id}')
                            img(src='#{item.poster}', alt='#{item.title}')
                        .caption
                            h3 #{item.title}
                            p: a.btn.btn-primary(href='/movie/#{item._id}', role='button')
                                观看预告片
```

list.jade

```
extends ../layout

block content
    .container
        .row
             table.table.table-hover.table-bordered
                thead
                    tr
                        th 电影名字
                        th 导演
                        th 国家
                        th 上映年份
                        //- th 录入时间
                        th 查看
                        th 更新
                        th 删除
                    tbody
                        each item in movies
                            tr(class='item-id-#{item._id}')
                                td #{item.title}
                                td #{item.doctor}
                                td #{item.country}
                                td #{item.year}
                                //- td #{moment(item.meta.createAt).format('MM/DD/YYYY')}
                                td: a(target='_blank', href='../movie/#{item._id}') 查看
                                td: a(target='_blank', href='../admin/update/#{item._id}') 修改
                                td
                                    button.btn.btn-danger.del(type='button', data-id='#{item._id}') 删除
```

## 项目数据库的实现

### mongodb 模式模型设计及编码

使用 mongoose 对 mongodb 进行操作

* Schema 模式定义：进行数据库每一个字段的定义

![](http://ojt6zsxg2.bkt.clouddn.com/0a6ed1fa1a328be7d0d20b580681401c.png)

* Model 编译模型，生成构造函数

![](http://ojt6zsxg2.bkt.clouddn.com/8c46e8bd40ac760f4a1e88a54f568337.png)

* Document：文档实例化

![](http://ojt6zsxg2.bkt.clouddn.com/d0b2004c48d1114beab8314ad3025353.png)

### 编写数据库 Schema 定义

model.js

```
let mongoose = require('mongoose');

let MovieSchema = new mongoose.Schema({
    doctor: String,
    title: String,
    language: String,
    summary: String,
    flash: String,
    poster: String,
    year: String,
    meta: {
        createAt: {
            type: DAte,
            default: Data.now(),
        },
        updateAt: {
            type: Data,
            default: Date.now(),
        },
    },
});

MovieSchema.pre('save', function(next) {
    if (this.isNew) {
        this.meta.createAt = this.meta.updateAt = Data.now();
    } else {
        this.meta.updateAt = Data.now();
    }
});

MovieSchema.statics = {
    fetch: function(cb) {
        return this.find({})
        .sort('meta.updataAt')
        .exec(cb);
    },
    findById: function(id, cb) {
        return this.findOne({_id, id})
        .exec(cb);
    },
};

module.exports = MovieSchema;
```

### 编写数据库编译模型，生成构造函数

```
let mongoose = require('mongoose');
let MovieSchema = require('../schemas/model');
let Movie = mongoose.model('Moive', MovieSchema);

module.exports = Movie;
```

### 编写数据库交互代码

主要的数据库交互逻辑都在 app.js 里面：

```
let express = require('express');
let path = require('path');
let serveStatic = require('serve-static');
let bodyPaerser = require('body-parser');
let underScore = require('underscore');
let mongoose = require('mongoose');

let Movie = require('./models/movie');
mongoose.Promise = global.Promise;
mongoose.connect('mongodb://127.0.0.1:27017/test');

let port = process.env.PORT || 3000;
let app = express();

app.set('views', './views/pages/');  // 应用的视图目录
app.set('view engine', 'jade'); // 应用的视图引擎
app.use(serveStatic('bower_components'));
app.use(bodyPaerser.urlencoded({extended: true}));
app.locals.moment = require('moment');
console.log('listen to port', port);
app.listen(port);


app.get('/', function(req, res) {
    Movie.fetch(function(err, movies) {
        if (err) {
            console.log(err);
        }
        res.render('index', {
            title: 'ShiningDan 主页',
            movies: movies,
        })
    })
});

app.get('/movie/:id', function(req, res) {   // 访问 /admin/3 返回 detail.jade 渲染后的效果
    let id = req.params.id;
    Movie.findById(id, function(err, movie) {
        if (err) {
            console.log(err);
        }
        res.render('detail', {
            title: movie.title,
            movie: movie,
        })
    })  
})

app.get('/admin/update/:id', function(req, res) {
    let id = req.params.id;
    if (id) {
        Movie.findById(id, function(err, movie) {
            res.render('admin', {
                title: 'shiningdan 后台更新页面',
                movie: movie,
            })
        })
    }
})


app.get('/admin/movie', function(req, res) {
    res.render('admin', {
        title: 'shiningdan 后台录入页',
        movie: {
            title: '',
            doctor: '',
            country: '',
            language: '',
            year: '',
            flash: '',
            poster: '',
            summary: '',
        }
    })
})

app.post('/admin/movie/new', function(req, res) {
    let movieObj = req.body.movie;
    let id = movieObj._id;
    let _movie;
    if (id !== 'undefined') {
        Movie.findById(id, function(err, movie) {
            if (err) {
                console.log(err);
            }
            _movie = underScore.extend(movie, movieObj);
            _movie.save(function(err, movie) {
                if (err) {
                    console.log(err);
                }
                res.redirect('/movie/' + movie._id);
            })
        })
    } else {
        _movie = Movie({
            doctor: movieObj.doctor,
            title: movieObj.title,
            country: movieObj.country,
            language: movieObj.language,
            year: movieObj.year,
            country: movieObj.country,
            poster: movieObj.poster,
            summary: movieObj.summary,
            flash: movieObj.flash,
        });
        // _id 在调用 Movie() 的时候会自动生成
        _movie.save(function(err, movie) {
            if (err) {
                console.log(err);
            }
            res.redirect('/movie/' + movie._id);
        })
    }
});


app.get('/admin/list', function(req, res) {  //访问 /admin/list 返回 list.jade 渲染后的效果
    Movie.fetch(function(err, movies) {
        if (err) {
            console.log(err);
        }
        res.render('list', {
            title: 'ShiningDan 列表页',
            movies: movies,
        })
    })
})
```

同时 list.jade 也修改了一些地方

```
extends ../layout

block content
    .container
        .row
             table.table.table-hover.table-bordered
                thead
                    tr
                        th 电影名字
                        th 导演
                        th 国家
                        th 上映年份
                        th 录入时间
                        th 查看
                        th 更新
                        th 删除
                    tbody
                        each item in movies
                            tr(class='item-id-#{item._id}')
                                td #{item.title}
                                td #{item.doctor}
                                td #{item.country}
                                td #{item.year}
                                td #{moment(item.meta.createAt).format('MM/DD/YYYY')}
                                td: a(target='_blank', href='../movie/#{item._id}') 查看
                                td: a(target='_blank', href='../admin/update/#{item._id}') 修改
                                td
                                    button.btn.btn-danger.del(type='button', data-id='#{item._id}') 删除
```

在定义 movie 结构的 model.js 里也添加了一些字段：

```
let mongoose = require('mongoose');

let MovieSchema = new mongoose.Schema({
    doctor: String,
    title: String,
    language: String,
    summary: String,
    flash: String,
    poster: String,
    year: String,
    country: String,
    meta: {
        createAt: {
            type: Date,
            default: Date.now(),
        },
        updateAt: {
            type: Date,
            default: Date.now(),
        },
    },
});

MovieSchema.pre('save', function(next) {
    if (this.isNew) {
        this.meta.createAt = this.meta.updateAt = Date.now();
    } else {
        this.meta.updateAt = Date.now();
    }
    next();
});

MovieSchema.statics = {
    fetch: function(cb) {
        return this.find({})
        .sort('meta.updateAt')
        .exec(cb);
    },
    findById: function(id, cb) {
        return this.findOne({_id: id})
        .exec(cb);
    },
};

module.exports = MovieSchema;
```

### 删除功能以及项目生成配置文件

删除的时候，在点击删除按钮时，用 jQuery 提交一个 AJAX 请求来删除数据库中相关的信息。

如果在根目录下还有一个 public 目录中也有静态资源，则应该把 `bower_components` 中的内容放在 public 下面。我们可以通过生成一个 `.bowerrc` 配置文件来指定 bower 的安装路径。

```
{
    "directory": "public/libs"
}
```

创建 admin.js，用来在前端接卸完成后对 `.del` 元素添加点击删除事件。admin.js 中的逻辑就是，当删除点击事件发生以后，发送一个 `DELETE` 的 AJAX 请求来请求后端从数据库中删除对应的电影信息。

```
$(function() {
    $('.del').click(function(event) {
        let target = $(event.target);
        let id = target.data('id');
        let tr = $('.item-id-' + id);

        $.ajax({
            type: 'DELETE',
            url: '/admin/list?id=' + id,
        })
        .done(function(result) {
            if (result.success === 1) {
                if(tr.length > 0) {
                    tr.remove();
                }
            }
        })
    })
})
```

然后在 `list.jade` 中引入 `admin.js`

```
extends ../layout

block content
    .container
        .row
             table.table.table-hover.table-bordered
                thead
                    tr
                        th 电影名字
                        th 导演
                        th 国家
                        th 上映年份
                        th 录入时间
                        th 查看
                        th 更新
                        th 删除
                    tbody
                        each item in movies
                            tr(class='item-id-#{item._id}')
                                td #{item.title}
                                td #{item.doctor}
                                td #{item.country}
                                td #{item.year}
                                td #{moment(item.meta.createAt).format('MM/DD/YYYY')}
                                td: a(target='_blank', href='../movie/#{item._id}') 查看
                                td: a(target='_blank', href='../admin/update/#{item._id}') 修改
                                td
                                    button.btn.btn-danger.del(type='button', data-id='#{item._id}') 删除
    script(src='/js/admin.js')
```

最后在 `app.js` 中添加对 `DELETE` AJAX 请求的响应：

```
app.delete('/admin/list', function(req, res) {
    let id = req.query.id;
    
    if (id) {
        Movie.remove({_id: id}, function(err, movie) {
            if (err) {
                console.log(err);
            } else {
                res.json({success: 1});
            }
        })
    }
})
```

可以使用 `bower init` 和 `npm init` 来生成项目的配置文件，这样就可以方便打包在其他地方部署。

整个项目的架构如下：

![](http://ojt6zsxg2.bkt.clouddn.com/351a29b687d7f38f527a429666e7abe3.png)

## Grunt 集成自动重启

Grunt 可以定义项目的自动处理流程，并且监听项目文件的变动自动热重启项目方便调试。

首先需要安装 Grunt:

```
npm install grunt --save-dev
npm install grunt-cli -g
npm install grunt-nodemon --save-dev
npm install grunt-concurrent--save-dev
```

然后在项目的根目录下生成 `gruntfile.js` 文件，内容如下：

```
module.exports = function(grunt) {

    grunt.initConfig({
        watch: {
            jade: {
                files: ['views/**'],
                options: {
                    livereload: true
                }
            },
            js: {
                files: ['public/js/**', 'models/**/*.js', 'schemas/**/*.js'],
                options: {
                    livereload: true,
                },
            }
        },
        nodemon: {
            dev: {
                script: 'app.js',
                options: {
                    args: [],
                    nodeArgs: ['--debug'],
                    ignore: ['README.md', 'node_modules/**', '.DS_Store'],
                    ext: 'js',
                    watch: ['./'],
                    delay: 1000,
                    env: {
                            PORT: '3000'
                    },
                    cwd: __dirname
                }
            }
        },

        concurrent: {
            tasks: ['nodemon', 'watch'],
            options: {
                logConcurrentOutput: true
            }
        },
    });

    grunt.loadNpmTasks('grunt-contrib-watch');
    grunt.loadNpmTasks('grunt-nodemon');
    grunt.loadNpmTasks('grunt-concurrent');
    
    grunt.option('force', true);
    grunt.registerTask('default', ['concurrent']);
}
```

运行 `grunt` 命令即可。

### 开发用户模型及密码处理

使用 bcrypt 来为用户的密码进行加盐和 hash 求值。

```
npm install --save bcrypt
```

创建 `schemas/user.js`，将 `schemas/movie.js` 中的内容拷贝进来，添加 bcrypt，并且在 `pre('save')` 中为用户密码加盐：

```
let bcrypt = require('bcrypt');
let SALT_WORK_FACTOR = 10;

MovieSchema.pre('save', function(next) {
    let user = this;
    if (this.isNew) {
        this.meta.createAt = this.meta.updateAt = Date.now();
    } else {
        this.meta.updateAt = Date.now();
    }
    bcrypt.genSalt(SALT_WORK_FACTOR, function(err, salt) {
        if (err) return next(err)

        bcrypt.hash(user.password, salt, function(err, hash) {
            if (err) return next(err);

            user.password = hash;
            next()
        })
    });
    next();
});
```

### 登录注册前端视图

登录的视图主要是在 header.jade 中添加 .navbar-fixed-bottom，实现在页面最下部添加注册与登录视图。点击注册与登录按钮，就会通过 bootstrap 的 modal 弹出遮罩层。

```
.container
    .row
        .page-header
            h1 #{title}
            small 重度科幻迷
.navbar.navbar-default.navbar-fixed-bottom
    .container
        .navbar-header
            a.navbar-brand(href="/") 重度科幻迷
        p.navbar-text.navbar-right
            a.navbar-link(href="#", data-toggle="modal", data-target="#signupModal") 注册
            span &nbsp;|&nbsp;
            a.navbar-link(href="#", data-toggle="modal", data-target="#signinModal") 登录
#signupModal.modal.fade
    .modal-dialog
        .modal-content
            form(method="POST", action="/user/signup")
                .modal-header 注册
                .modal-body
                    .form-group
                        lable(for="signupName") 用户名
                        input#singupName.form-control(name="user[name]", type="text")
                        lable(for="signupPassword") 密码
                        input#singupPassword.form-control(name="user[password]", type="text")
                    .modal-footer
                        button.btn.btn-default(type="button", data-dismiss="modal") 关闭
                        button.btn.btn-success(type="submit") 提交
#signinModal.modal.fade
    .modal-dialog
        .modal-content
            form(method="POST", action="/user/signin")
                .modal-header 登录
                .modal-body
                    .form-group
                        lable(for="signinName") 用户名
                        input#singinName.form-control(name="user[name]", type="text")
                        lable(for="signinPassword") 密码
                        input#singinPassword.form-control(name="user[password]", type="text")
                    .modal-footer
                        button.btn.btn-default(type="button", data-dismiss="modal") 关闭
                        button.btn.btn-success(type="submit") 提交
```

### 注册用户后台存储

前端给后端传输 userid 的方法有很多种：

1. 在 URL 中包含 userid 

```
app.post('/user/signup/:userid', function() {
    let _userid = req.params.userid;
});
```

这个样子就需要在 `req.params.userid` 中获取

2. 在 queryString 中包含 userid：

```
app.post('/user/signup/:userid', function() {
    ///user/signup/1111?userid=1112
    let _userid = req.query.userid;
});
```

遇到这种情况需要去 `req.query` 中去获取 userid

3. 通过 POST 中传  userid，可以去 `req.body` 中获取：

```
app.post('/user/signup/:userid', function() {
    let userid = req.body.userid;
});
```

4. 统一使用 `req.param` 来获取 userid 的方法，如果传入的参数如下，有在 URL 中有 userid，在 queryString 中也有 userid，异步提交的数据中也有 userid (在 body) 里：

```
app.post('/user/signup/:userid', function() {
    ///user/signup/1111?userid=1112
    // body {userid: 1113}
    let userid = req.param.userid;
});
```

在这种情况下，express 中获得 userid 的优先级是：

```
URL > body > queryString
```

#### 对 User 生成构造函数

在 `/models` 中添加 `user.js`

```
let mongoose = require('mongoose');
let UserSchema = require('../schemas/user');
let User = mongoose.model('User', UserSchema);

module.exports = User;
```

并且导入到 `app.js` 中：

```
let User = require('./models/user');
```

在 `app.js` 中完成对 `POST` 请求的处理，如果该用户存在，则定向到 `/`，如果该用户不存在，子啊 mongodb 中创建该用户，并且重定向到 `/admin/userlist`：

```
app.post('/user/signup', function(req, res) {
    let userid = req.body.user;

    let user = new User(userid);

    User.find({name: user.name}, function(err, user) {
        if (err) {
            console.log(err);
        }

        if (user) {
            return res.redirect('/');
        } else {
            user.save(function(err, user) {
                if (err) {
                    console.log(err);
                }
                res.redirect('/admin/userlist')
            });
        }
    });
});

app.get('/admin/userlist', function(req, res) { 
    User.fetch(function(err, users) {
        if (err) {
            console.log(err);
        }
        res.render('userlist', {
            title: 'ShiningDan 列表页',
            users: users,
        })
    })
})
```

然后在 `/views/pages` 中添加 `userlist.jade` 的模板，但是此时还没有处理查看/修改/删除功能。：

```
extends ../layout

block content
    .container
        .row
             table.table.table-hover.table-bordered
                thead
                    tr
                        th 名字
                        th 时间
                        th 查看
                        th 更新
                        th 删除
                    tbody
                        each item in users
                            tr(class='item-id-#{item._id}')
                                td #{item.name}
                                td #{moment(item.meta.createAt).format('MM/DD/YYYY')}
                                td: a(target='_blank', href='../movie/#{item._id}') 查看
                                td: a(target='_blank', href='../admin/update/#{item._id}') 修改
                                td
                                    button.btn.btn-danger.del(type='button', data-id='#{item._id}') 删除
    script(src='/js/admin.js')
```

### 实现登录逻辑

为了实现登录的逻辑，我们需要对 `/user/login` 的 POST 请求路由进行处理。

```
app.post('/user/signin', function(req, res) {
    let _user = req.body.user;
    let name = _user.name;
    let password = _user.password;

    User.findOne({name: name}, function(err, user) {
        if (err) {
            console.log(err);
        }
        if (!user) {
            return res.redirect('/');
        }
        user.comparePassword(password, function(err, isMatch) {
            if (err) {
                console.log(err);
            }
            if (isMatch) {
                console.log("Password is matched");
                res.redirect('/');
            } else {
                console.log("Password is not matched");
            }
        })
    })
});
```

然后在 `schemas/user.js` 中创建实例方法 `comparePassword` ，来进行密码比对：

```
//实例方法，只有在实例中才能调用
UserSchema.methods = {
    comparePassword: function(_password, cb) {
        bcrypt.compare(_password, this.password, function(err, isMatch) {
            if (err) {
                return cb(err);
            }
            cb(null, isMatch);
        })
    }
};
```

### 保持用户登录状态

可以在 session 中存储用户的登录信息。首先导入 express-session 模块：

```
let session = require('express-session');
```

然后在 express 启动后使用该中间件：

```
app.use(session({
    secret: 'zyc',
    resave: false,
    saveUninitialized: true,
}));
```

当用户登录以后，把用户的登录验证信息放在 `req.session.user` 中：

```
user.comparePassword(password, function(err, isMatch) {
    if (err) {
        console.log(err);
    }
    if (isMatch) {
        req.session.user = user;

        res.redirect('/');
    } else {
        console.log("Password is not matched");
    }
})
```

然后在 `/` 路由的处理中可以打印得到 `req.session.user`：

```
app.get('/', function(req, res) {
    console.log("user in session");
    console.log(req.session.user);
    Movie.fetch(function(err, movies) {
        if (err) {
            console.log(err);
        }
        res.render('index', {
            title: 'ShiningDan 主页',
            movies: movies,
        })
    })
});
```

但是，此时 session 并没有做持久化存储，当页面刷新以后，该 session 就会消失，所以要在 mongodb 中存储该用户的登录。首先导入 connect-mongo 模块：

```
let mongoStore = require('connect-mongo')(session);
```

当对 session 进行存储的时候，可以使用 connect-mongo 模块对 session 数据进行自动化存储：

```
app.use(session({
    secret: 'zyc',
    resave: false,
    saveUninitialized: true,
    store: new mongoStore({
        url: dbUrl,
        collection: 'sessions',
    }),
}));
```

此时，每当我们在 req.session 中存储一个新的数据后，就会在 mongodb 中的 sessions 表内创建一个新的内容，用来存储该会话，即使是页面重新刷新也存在。

![](http://ojt6zsxg2.bkt.clouddn.com/8d0be6673c36b57de18e4497d74f0bf8.png)

### 注销用户，用户退出功能实现

为了实现用户注销的功能，需要在 header.jade 中修改页面结构，判断用户是否登陆过：

```
.navbar.navbar-default.navbar-fixed-bottom
    .container
        .navbar-header
            a.navbar-brand(href="/") 重度科幻迷
        if user
            p.navbar-text.navbar-right
                span 欢迎您，#{user.name}
                span &nbsp;|&nbsp;
                a.navbar-link(href="/logout") 登出
        else
            p.navbar-text.navbar-right
                a.navbar-link(href="#", data-toggle="modal", data-target="#signupModal") 注册
                span &nbsp;|&nbsp;
                a.navbar-link(href="#", data-toggle="modal", data-target="#signinModal") 登录
```

这里 `if user` 判断的是在 `app.locals.user` 中是否已经有值，如果有值，则渲染登出部分模板。如果没有值，就渲染登录部分模板。

创建 `/logout` 路由的处理方法：

```
// logout 
app.get('/logout', function(req, res) {
    delete req.session.user;
    delete app.locals.user;
    res.redirect('/');
})
```

并且在 `/` 中添加判断 `req.sesison.user` 中是否有值得判断，如果有值，则将 user 的值赋值给 `app.locals.user`

```
app.get('/', function(req, res) {
    console.log("user in session");
    console.log(req.session.user);
    let _user = req.session.user;

    if(_user) {
        app.locals.user = _user;
    }
    ...
}
```

### 会话持久的预处理

目前路由在添加 `req.locals.user` 的部分是在 `/` 下面，但是在其他的页面登录就不会进行保存。所以要在所有的页面都添加 `req.locals.user`，要在 `app.use` 中进行预处理：

```
app.use(function(req, res, next) {
    let _user = req.session.user;

    if(_user) {
        app.locals.user = _user;
    }
    next()
});
```

### 调整路由结构，独立路由处理层

将所有路由相关的逻辑都放在了 `/config/route.js` 逻辑下，然后通过 `module.exports` 导出。在 `app.js` 中导入 `route.js` 模块，并且通过 `require` 引入 `route.js`

在 `app.js` 中

```
require('./config/route')(app);
```

在 `/config/route.js` 中：

```
let Movie = require('../models/movie');
let User = require('../models/user');

module.exports = function(app) {
    app.use(function(req, res, next) {
        let _user = req.session.user;

        if(_user) {
            app.locals.user = _user;
        }
        next()
    });
    ...
}
```

### 配置入口文件

在本地开发环境中，可以添加一些配置，方便本地调试。在 `app.js` 中添加如下的代码：

```
let morgan = require('morgan');
if ('development' === app.get('env')) {
    app.set('showStackError', true);    // 将本地运行的错误打印出来
    app.use(morgan(':method :url :status')); //将 express 的日志，每个请求的类型，路径，状态值打印出来
    app.locals.pretty = true;  // 页面的源码设置为不格式化，不压缩
    mongoose.set('debug', true);   // 打开 mongodb 的 debug 模式，显示每一次请求
}
```

### 调整目录结构，彻底分离 MVC 层

现在所有的路由的处理都是在 `route.js` 中执行，我们可以把 `route.js` 中所有的处理逻辑分成 `user.js`、`movie.js`、`index.js`，然后把对应的路由处理逻辑放在其中，都放在 `/app/controllers`里面，把 `、view`  文件夹放在 `/app/view` 这里，把 `/models` 和 `/schemas` 文件夹都放在 `/app` 文件夹下。。最后修改 `app.js` 中视图的目录，调整为：

```
app.set('views', './app/views/pages/');  // 应用的视图目录
```

最后项目的结构和部分文件的内容如下：

![](http://ojt6zsxg2.bkt.clouddn.com/f4b6115078e0b57eb479c5563e2ea0f3.png)

`route.js`

```
let Index = require('../app/controllers/index');
let User = require('../app/controllers/user');
let Movie = require('../app/controllers/movie');

module.exports = function(app) {
    app.use(function(req, res, next) {
        let _user = req.session.user;
        app.locals.user = _user;
        
        next()
    });

    app.get('/', Index.index);

    app.post('/user/signin', User.signin);
    app.post('/user/signup', User.signup);
    app.get('/logout', User.logout);
    app.get('/admin/userlist', User.list);

    app.get('/movie/:id', Movie.detail);
    app.get('/admin/update/:id', Movie.update);
    app.get('/admin/movie', Movie.save);
    app.post('/admin/movie/new', Movie.new);
    app.get('/admin/list', Movie.list);
    app.delete('/admin/list', Movie.del)
}
```

`index.js`：

```

let Movie = require('../models/movie');

exports.index = function(req, res) {
    console.log("user in session");
    console.log(req.session.user);

    Movie.fetch(function(err, movies) {
        if (err) {
            console.log(err);
        }
        res.render('index', {
            title: 'ShiningDan 主页',
            movies: movies,
        })
    })
}
```

`movie.js`

```
let Movie = require('../models/movie');

exports.detail = function(req, res) {   // 访问 /admin/3 返回 detail.jade 渲染后的效果
    let id = req.params.id;
    Movie.findById(id, function(err, movie) {
        if (err) {
            console.log(err);
        }
        res.render('detail', {
            title: movie.title,
            movie: movie,
        })
    })  
}

exports.update = function(req, res) {
    let id = req.params.id;
    if (id) {
        Movie.findById(id, function(err, movie) {
            res.render('admin', {
                title: 'shiningdan 后台更新页面',
                movie: movie,
            })
        })
    }
}

exports.save = function(req, res) {
    res.render('admin', {
        title: 'shiningdan 后台录入页',
        movie: {
            title: '',
            doctor: '',
            country: '',
            language: '',
            year: '',
            flash: '',
            poster: '',
            summary: '',
        }
    })
}

exports.new = function(req, res) {
    let movieObj = req.body.movie;
    let id = movieObj._id;
    let _movie;
    if (id !== 'undefined') {
        Movie.findById(id, function(err, movie) {
            if (err) {
                console.log(err);
            }
            _movie = underScore.extend(movie, movieObj);
            _movie.save(function(err, movie) {
                if (err) {
                    console.log(err);
                }
                res.redirect('/movie/' + movie._id);
            })
        })
    } else {
        _movie = Movie({
            doctor: movieObj.doctor,
            title: movieObj.title,
            country: movieObj.country,
            language: movieObj.language,
            year: movieObj.year,
            country: movieObj.country,
            poster: movieObj.poster,
            summary: movieObj.summary,
            flash: movieObj.flash,
        });
        // _id 在调用 Movie() 的时候会自动生成
        _movie.save(function(err, movie) {
            if (err) {
                console.log(err);
            }
            res.redirect('/movie/' + movie._id);
        })
    }
}

exports.list = function(req, res) {  //访问 /admin/list 返回 list.jade 渲染后的效果
    Movie.fetch(function(err, movies) {
        if (err) {
            console.log(err);
        }
        res.render('list', {
            title: 'ShiningDan 列表页',
            movies: movies,
        })
    })
}

exports.del = function(req, res) {
    let id = req.query.id;
    
    if (id) {
        Movie.remove({_id: id}, function(err, movie) {
            if (err) {
                console.log(err);
            } else {
                res.json({success: 1});
            }
        })
    }
}
```

`user.js`

```
let User = require('../models/user');

exports.signin = function(req, res) {
    let _user = req.body.user;
    let name = _user.name;
    let password = _user.password;

    User.findOne({name: name}, function(err, user) {
        if (err) {
            console.log(err);
        }
        if (!user) {
            return res.redirect('/');
        }
        user.comparePassword(password, function(err, isMatch) {
            if (err) {
                console.log(err);
            }
            if (isMatch) {
                req.session.user = user;

                res.redirect('/');
            } else {
                console.log("Password is not matched");
            }
        })
    })
}

exports.signup = function(req, res) {
    let userid = req.body.user;

    let user = new User(userid);
    User.findOne({name: user.name}, function(err, user) {
        if (err) {
            console.log(err);
        }

        if (user) {
            return res.redirect('/');
        } else {
            user.save(function(err, user) {
                if (err) {
                    console.log(err);
                }
                res.redirect('/admin/userlist')
            });
        }
    });
}

exports.logout = function(req, res) {
    delete req.session.user;
    // delete app.locals.user;
    res.redirect('/');
}

exports.list = function(req, res) { 
    User.fetch(function(err, users) {
        if (err) {
            console.log(err);
        }
        res.render('userlist', {
            title: 'ShiningDan 列表页',
            users: users,
        })
    })
}
```

### 增加注册和登录跳转页面

添加注册模板 `signup.jade` 和登录模板 `signin.jade`：

`signup.jade`

```
extends ../layout

block content
    .container
        .row
            .col-md-5
                form(method="POST", action="/user/signup")
                    .modal-body
                        .form-group
                            lable(for="signinName") 用户名
                            input#singinName.form-control(name="user[name]", type="text")
                            lable(for="signinPassword") 密码
                            input#singinPassword.form-control(name="user[password]", type="text")
                        .modal-footer
                            button.btn.btn-default(type="button", data-dismiss="modal") 关闭
                            button.btn.btn-success(type="submit") 提交
```

`signin.jade`

```
extends ../layout

block content
    .container
        .row
            .col-md-5
                form(method="POST", action="/user/signin")
                    .modal-body
                        .form-group
                            lable(for="signinName") 用户名
                            input#singinName.form-control(name="user[name]", type="text")
                            lable(for="signinPassword") 密码
                            input#singinPassword.form-control(name="user[password]", type="text")
                        .modal-footer
                            button.btn.btn-default(type="button", data-dismiss="modal") 关闭
                            button.btn.btn-success(type="submit") 提交
```

然后在 `route.js` 中添加对该模板的路由解析：

```
    app.get('/signin', User.showSignin);
    app.get('/signup', User.showSignup);
```

在 `user.js` 中添加 `showSignin` 和 `showSignup` 方法来渲染模板：

```
exports.showSignin = function(req, res) {
    res.render('signin', {
        title: '登录页面',
    });
}

exports.showSignup = function(req, res) {
    res.render('signup', {
        title: '注册页面',
    });
}
```

修改原来的 `signin` 方法和 `signup` 方法，重定向到这两个新的页面：

```
exports.signin = function(req, res) {
    let _user = req.body.user;
    let name = _user.name;
    let password = _user.password;

    User.findOne({name: name}, function(err, user) {
        if (err) {
            console.log(err);
        }
        if (!user) {
            return res.redirect('/signup');
        }
        user.comparePassword(password, function(err, isMatch) {
            if (err) {
                console.log(err);
            }
            if (isMatch) {
                req.session.user = user;

                res.redirect('/');
            } else {
                res.redirect('/signin');
                console.log("Password is not matched");
            }
        })
    })
}
exports.signup = function(req, res) {
    let userid = req.body.user;

    let user = new User(userid);
    User.findOne({name: user.name}, function(err, user) {
        if (err) {
            console.log(err);
        }

        if (user) {
            return res.redirect('/signin');
        } else {
            user.save(function(err, user) {
                if (err) {
                    console.log(err);
                }
                res.redirect('/')
            });
        }
    });
}
```

### 用户权限管理

首先，在 `/schemas/user.js` 中给用户添加一个 role 字段，用来代表不同等级的用户：

```
// 0: normal user
// 1: verified user
// 2: professional user
// >10: admin
// > 50: super admin
role: {
    type: Number,
    default: 0,
},
```

然后，在访问 `/admin/` 开头的 url 中，都使用中间件对用户的 url 进行判断，在 `/app/controllers/user.js` 中定义验证用户登录的中间件和验证用户权限的中间件：

```
//middleware for user
exports.signinRequired = function(req, res, next) {
    let user = req.session.user;
    if (!user) {
        return res.redirect('/signin');
    }
    next();
}

exports.adminRequired = function(req, res, next) {
    let user = req.session.user;
    if(user.role <= 10) {
        return res.redirect('/signin');
    }
    next();
}
```

对所有的 `/admin` url 进行修改，整理对外访问的 url 的格式：

```
    app.get('/admin/user/list', User.signinRequired, User.adminRequired, User.list);

    app.get('/movie/:id', Movie.detail);
    app.get('/admin/movie/update/:id', User.signinRequired, User.adminRequired, Movie.update);
    app.get('/admin/movie', User.signinRequired, User.adminRequired, Movie.save);
    app.post('/admin/movie/new', User.signinRequired, User.adminRequired, Movie.new);
    app.get('/admin/movie/list', User.signinRequired, User.adminRequired, Movie.list);
    app.delete('/admin/movie/list', User.signinRequired, User.adminRequired, Movie.del)
```

并且修改 `/public/js/admin.js` 中删除的路径为新的路径：

```
$.ajax({
    type: 'DELETE',
    url: '/admin/movie/list?id=' + id,
})
```

## 开发评论功能

### 设计评论的数据模型

在页面中显示的评论需要被存储到数据库中，所以需要为评论定义一个合适的模型，模型中需要包含的字段有：

1. 这条评论是在哪个 movie 下面的
2. 这条评论是谁发送的 from
3. 这条评论是评论给谁的 to 
4. 这条评论的内容是什么

所以在 `/schemas/` 中创建 `comment.js`，用来定义评论的模型：

```
let mongoose = require('mongoose');
let Schema = mongoose.Schema;
let ObjectId = Schema.Types.ObjectId;

let CommentSchema = new Schema({
    movie: {
        type: ObjectId,
        ref: 'Movie',  // ObjectId 指向 Movi 中的数据
    },
    from : {
        type: ObjectId,
        ref: 'User',
    },
    to : {
        type: ObjectId,
        ref: 'User',
    },
    content: String,
    meta: {
        createAt: {
            type: Date,
            default: Date.now(),
        },
        updateAt: {
            type: Date,
            default: Date.now(),
        },
    },
});

CommentSchema.pre('save', function(next) {
    if (this.isNew) {
        this.meta.createAt = this.meta.updateAt = Date.now();
    } else {
        this.meta.updateAt = Date.now();
    }
    next();
});

CommentSchema.statics = {
    fetch: function(cb) {
        return this.find({})
        .sort('meta.updateAt')
        .exec(cb);
    },
    findById: function(id, cb) {
        return this.findOne({_id: id})
        .exec(cb);
    },
};

module.exports = CommentSchema;
```

### 评论存储、查询与展现

在 `/app/models` 中创建 `comment.js`，内容为创建 Comment 的构造函数：

```
let mongoose = require('mongoose');
let CommentSchema = require('../schemas/comment');
let Comment = mongoose.model('Comment', CommentSchema);

module.exports = Comment;
```

在 `route.js` 中创建对 `/admin/comment` URL 的处理，用来处理对 comment 的 POST 请求：

```
app.post('/user/comment', User.signinRequired, Comment.save);
```

然后在 `/app/controllers/` 中创建 `comment.js` 来处理 post 请求：

```
let Comment = require('../models/comment');

exports.save = function(req, res) {
    let _comment = req.body.comment;
    let comment = new Comment(_comment);
    let movieId = _comment.movie;

    comment.save(function(err, comment) {
        if (err) {
            console.log(err);
        }
        res.redirect('/movie/'+movieId);
    });
}
```

在 `detail.jade` 模板中添加评论的部分，包括评论的显示部分和一个发表评论的部分：

```
extends ../layout

block content
    .container
        .row
            .col-md-7
                embed(src='#{movie.flash}', allowFullScreen='true', quality='high', width='720', height='600', align='middle', type='application/x-shockwave-flash')
                .panel.panel-default
                    .panel-heading
                        h3 评论区
                    .panel-body
                        ul.media-list
                            each item in comments
                                li.media
                                    .pull-left
                                        img.media-object(src='', style="width:64px;height:64px;")
                                    .media-body
                                    h4.media-heading #{item.from.name}
                                    p #{item.content}
                                hr
                        form(method='POST', action='/user/comment')
                            input(type='hidden', name='comment[movie]', value='#{movie._id}')
                            input(type='hidden', name='comment[from]', value='#{user._id}')
                            .form-group
                                textarea.form-control(name='comment[content]', row='3')
                            button.btn.btn-primary(type='submit') 提交
            .col-md-5
                dl.dl-horizontal
                    dt 电影名字
                    dd #{movie.title}
                    dt 导演
                    dd #{movie.doctor}
                    dt 国家
                    dd #{movie.country}
                    dt 语言
                    dd #{movie.language}
                    dt 上映年份
                    dd #{movie.year}
                    dt 简介
                    dd #{movie.summary}
```

然后在 `detail.jade` 被渲染的时候，也就是在 `/app/controllers/movie.js` 中的 `detail` 函数中，通过获得的 movie，找到对应的评论，然后通过评论找到用户，传入用户的名字，最后交给 `detail.jade` 渲染出来。

```
exports.detail = function(req, res) {   // 访问 /admin/3 返回 detail.jade 渲染后的效果
    let id = req.params.id;
    Movie.findById(id, function(err, movie) {
        if (err) {
            console.log(err);
        }
        Comment.find({movie: id})
        .populate('from', 'name')
        .exec(function(err, comments) {
            res.render('detail', {
                title: movie.title,
                movie: movie,
                comments: comments
            })
        });
    })  
}
```

### 用户之间的相互回复功能

当需要显示用户之间的评论和在评论下发表的子评论时，需要修改评论的数据库模型，在 Comment 中存储子评论：

```
let CommentSchema = new Schema({
    movie: {
        type: ObjectId,
        ref: 'Movie',  // ObjectId 指向 Movi 中的数据
    },
    from : {
        type: ObjectId,
        ref: 'User',
    },
    to : {
        type: ObjectId,
        ref: 'User',
    },
    reply: [{
        from: {type: ObjectId, ref: 'User'},
        to: {type: ObjectId, ref: 'User'},
        content: String,
    }],
    content: String,
    meta: {
        createAt: {
            type: Date,
            default: Date.now(),
        },
        updateAt: {
            type: Date,
            default: Date.now(),
        },
    },
});
```

然后修改 `detail.jade`，添加子评论的部分。在原来的用户头像 `img` 标签外扩展一个 `a` 标签，当点击这个 `a` 标签的时候，会跳转到评论输入区域。

```
extends ../layout

block content
    .container
        .row
            .col-md-7
                embed(src='#{movie.flash}', allowFullScreen='true', quality='high', width='720', height='600', align='middle', type='application/x-shockwave-flash')
                .panel.panel-default
                    .panel-heading
                        h3 评论区
                    .panel-body
                        ul.media-list
                            each item in comments
                                li.media
                                    .pull-left
                                        a.comment(href='#comments', data-cid='#{item._id}', data-tid='#{item.from._id}')
                                            img.media-object(src='', style="width:64px;height:64px;")
                                    .media-body
                                        h4.media-heading #{item.from.name}
                                        p #{item.content}
                                        if item.reply && item.reply.length > 0
                                            each reply in item.reply
                                                .media
                                                    .pull-left
                                                        a.comment(href='#comments', data-cid='#{item._id}', data-tid='#{reply.from._id}')
                                                            img.media-object(src='', style="width:64px;height:64px;")
                                                    .media-body
                                                    h4.media-heading 
                                                        | #{reply.from.name}
                                                        span.text-info &nbsp;回复&nbsp;
                                                        | #{reply.to.name} :
                                                    p #{reply.content}
                                hr
                    #comment
                        form#commentForm(method='POST', action='/user/comment')
                            input(type='hidden', name='comment[movie]', value='#{movie._id}')
                            input(type='hidden', name='comment[from]', value='#{user._id}')
                            .form-group
                                textarea.form-control(name='comment[content]', row='3')
                            button.btn.btn-primary(type='submit') 提交
            .col-md-5
                dl.dl-horizontal
                    dt 电影名字
                    dd #{movie.title}
                    dt 导演
                    dd #{movie.doctor}
                    dt 国家
                    dd #{movie.country}
                    dt 语言
                    dd #{movie.language}
                    dt 上映年份
                    dd #{movie.year}
                    dt 简介
                    dd #{movie.summary}
    script(src='/js/detail.js')
```

然后创建一个新的 js 文件叫 `/public/js/detail.js` 在 `.comment` 上面绑定一个事件，事件的内容是，如果点击了该用户的头像，就会在评论区添加隐藏的 `input` 标签，表示这是对某个用户的评论：

```
$(function() {
    $('.comment').click(function(e) {
        let target = $(this);
        let toId = target.data('tid');
        let commentId = target.data('cid');

        if ($('#toId').length > 0) {
            $('#toId').val(toId);
        } else {
            $('<input>').attr({
                type: 'hidden',
                id: 'toId',
                name: 'comment[tid]',
                value: toId,
            }).appendTo('#commentForm');
        }
        if ($('#commentId').length > 0) {
            $('#commentId').val(toId);
        } else {
            $('<input>').attr({
                type: 'hidden',
                id: 'commentId',
                name: 'comment[cid]',
                value: commentId,
            }).appendTo('#commentForm');
        }
    })
});
```

然后在处理 `comment` 的路由里面，添加对 `tId` 和 `cId` 的处理：

```
let Comment = require('../models/comment');

exports.save = function(req, res) {
    let _comment = req.body.comment;
    let movieId = _comment.movie;

    if(_comment.cid) {
        Comment.findById(_comment.cid, function(err, comment) {
            console.log(comment);
            if (comment) {
                let reply = {
                    from: _comment.from,
                    to: _comment.tid,
                    content: _comment.content,
                };

                comment.reply.push(reply);

                comment.save(function(err, comment) {
                    if(err) {
                        console.log(err);
                    }
                    res.redirect('/movie/' + movieId);
                })
            }
        });
    } else {
        let comment = new Comment(_comment);
        comment.save(function(err, comment) {
            if (err) {
                console.log(err);
            }
            res.redirect('/movie/'+movieId);
        });
    } 
}
```

在处理 `detail.jade` 的 `Movie.detail` 函数中，添加对子评论的查找以及显示的功能：

```
exports.detail = function(req, res) {   // 访问 /admin/3 返回 detail.jade 渲染后的效果
    let id = req.params.id;
    Movie.findById(id, function(err, movie) {
        if (err) {
            console.log(err);
        }
        Comment.find({movie: id})
        .populate('from', 'name')
        .populate('reply.from reply.to', 'name')
        .exec(function(err, comments) {
            res.render('detail', {
                title: movie.title,
                movie: movie,
                comments: comments
            })
        });
    })  
}
```

### 对评论做登录限制

当用户没有登录的时候，不能显示评论按钮，而是显示登陆后评论，在 `detail.jade` 中进行修改：

```
#comment
                        form#commentForm(method='POST', action='/user/comment')
                            input(type='hidden', name='comment[movie]', value='#{movie._id}')
                            if user 
                                input(type='hidden', name='comment[from]', value='#{user._id}')
                            .form-group
                                textarea.form-control(name='comment[content]', row='3')
                            if user
                                button.btn.btn-primary(type='submit') 提交
                            else
                                a.navbar-link(href="#", data-toggle="modal", data-target="#signinModal") 登录后评论 
```

显示效果如下，点击**登录后评论**，会弹出登录对话窗：

![](http://ojt6zsxg2.bkt.clouddn.com/914cf28d10c02444eb9a8ed85afab819.png)

## 实现电影的分类功能

### 设计分类的数据模型

单独建立一个分类的表，管理分类的名字、分类的添加和删除，将电影的表和分类的表建立关系，在 `/schemas` 中创建 `category.js` 文件：

```
let mongoose = require('mongoose');
let Schema = mongoose.Schema;
let ObjectId = Schema.Types.ObjectId;

let CategorySchema = new Schema({
    name: String,
    movies: [{
        type: ObjectId,
        ref: 'Movie',
    }],
    meta: {
        createAt: {
            type: Date,
            default: Date.now(),
        },
        updateAt: {
            type: Date,
            default: Date.now(),
        },
    },
});

CategorySchema.pre('save', function(next) {
    if (this.isNew) {
        this.meta.createAt = this.meta.updateAt = Date.now();
    } else {
        this.meta.updateAt = Date.now();
    }
    next();
});

CategorySchema.statics = {
    fetch: function(cb) {
        return this.find({})
        .sort('meta.updateAt')
        .exec(cb);
    },
    findById: function(id, cb) {
        return this.findOne({_id: id})
        .exec(cb);
    },
};

module.exports = CategorySchema;
```

### 分类后台录入及分类存储

创建 `/models/category.js` 来创建 `category` 的模型：

```
let mongoose = require('mongoose');
let CategorySchema = require('../schemas/category');
let Category = mongoose.model('Category', CategorySchema);

module.exports = Category;
```

首先创建 admin 的分类录入模板 `category_admin.jade`，在访问 `/admin/category/new` 的时候返回该模板的渲染效果，在 `route.js` 中创建对分类的路由处理：

`category_admin.jade`

```
extends ../layout

block content
    .container
        .row
            form.form-horizontal(method='post', action='/admin/category/new')
                .from-group
                    label.col-sm-2.control-label(for='inputCategory') 电影分类
                    .col-sm-10
                        input#inputCategory.form-control(type='text', name='category[name]', value=category.name)
                .form-group
                    .col-sm-offset-2.col-sm-10
                    button.btn.btn-default(type='submit') 录入
```

然后创建对 `category_admin.jade` 渲染的路由处理，在 `/controllers` 下面创建 `category.js`，创建 `new` 函数来处理 `category_admin` 的渲染：

`category.js`

```
exports.new = function(req, res) {
    res.render('category_admin', {
        title: 'shiningdan 后台分类录入页',
        category: {},
    });
}
```

然后在 `route.js` 中将 `/admin/category/new` 的 get 请求对应 `new` 函数进行处理：

```
let Category = require('../app/controllers/category');

app.get('/admin/category/new', User.signinRequired, User.adminRequired, Category.new);
```

然后对 `/admin/category/new` 的 POST 请求进行处理，将得到添加分类的请求传输到数据库中：

`category.js`

```
let Category = require('../models/category');

exports.save = function(req, res) {
    let _category = req.body.category;
    let category = new Category(_category);

    category.save(function(err, category) {
        if (err) {
            console.log(err);
        }
        res.redirect('/admin/category/list');
    })
}
```

在新添加完分类以后，路由会被从定向到 `/admin/category/list`，所以要在  `route.js` 中创建对 `/admin/category/list` 的 GET 请求的处理：

`route.js`

```
app.post('/admin/category/list', User.signinRequired, User.adminRequired, Category.save);
app.get('/admin/category/list', User.signinRequired, User.adminRequired, Category.list);
```

`category.js`

```

```

`list` 函数需要渲染一个新的模板来显示分类页面，所以在 `/app/views/pages/` 下面创建一个 `categorylist/jade` 来处理所有的 Category 输出的渲染：

`categorylist.jade`

```
extends ../layout

block content
    .container
        .row
             table.table.table-hover.table-bordered
                thead
                    tr
                        th 名字
                        th 时间
                        th 查看
                        th 更新
                        th 删除
                    tbody
                        each item in categories
                            tr(class='item-id-#{item._id}')
                                td #{item.name}
                                td #{moment(item.meta.createAt).format('MM/DD/YYYY')}
                                td: a(target='_blank', href='../movie/#{item._id}') 查看
                                td: a(target='_blank', href='../admin/update/#{item._id}') 修改
                                td
                                    button.btn.btn-danger.del(type='button', data-id='#{item._id}') 删除
    script(src='/js/admin.js')
```

### 电影录入增加分类选择

在电影录入的模板 `admin.jade` 中添加关于电影分类的选取部分：

```
form.form-horizontal(method='post', action='/admin/movie/new')
                if movie._id
                    input(type='hidden', name='movie[_id]', value='#{movie._id}')
                .from-group
                    label.col-sm-2.control-label(for='inputCategory') 电影分类
                    .col-sm-10
                        input#inputTitle.form-control(type='text', name='movie[categoryName]', value='#{movie.categoryName}')    
                .form-group
                    label.col-sm-2.control-label 分类选择
                    each cat in categories
                        label.radio-inline
                            if movie._id
                                input(type='radio', name='movie[category]', value=cat._id, checked=cat._id.toString()==movie.category.toString())
                            else
                                input(type='radio', name='movie[category]', value=cat._id)
                            | #{cat.name}    
                .from-group
                    label.col-sm-2.control-label(for='inputTitle') 电影名字
                    .col-sm-10
                        input#inputTitle.form-control(type='text', name='movie[title]', value='#{movie.title}')
```

在 `/app/schemas/movie.js` 中添加 category 字段：

```
category: {
    type: ObjectId,
    ref: 'Category',
},
```

在 `movie.new` 方法中，需要在对 `admin.jade` 模板进行初始化的时候传入 `categories` 值：

```
exports.new = function(req, res) {
    Category.find({}, function(err, categories) {
        res.render('admin', {
            title: 'shiningdan 后台录入页',
            movie: {},
            categories: categories,
        })
    });
}
```

然后在 `admin.jade` 中处理所有的 value，将 `value='#{movie.language}'` 替换为 `value=movie.language`，不然在页面显示中会有 `undefined` 出现。

然后，在 `movie.save` 方法中，需要处理对分类的 post 请求，在存储 movie 的数据的时候，也要在 category 中将该 movie 添加进去：

`/app/controllers/movie.js`

```
exports.save = function(req, res) {
    let movieObj = req.body.movie;
    let id = movieObj._id;
    let _movie;
    if (id) {
        Movie.findById(id, function(err, movie) {
            if (err) {
                console.log(err);
            }
            _movie = underScore.extend(movie, movieObj);
            _movie.save(function(err, movie) {
                if (err) {
                    console.log(err);
                }
                res.redirect('/movie/' + movie._id);
            })
        })
    } else {
        _movie = Movie(movieObj);
        // _id 在调用 Movie() 的时候会自动生成
        let categoryId = _movie.category;
        _movie.save(function(err, movie) {
            if (err) {
                console.log(err);
            }
            Category.findById(categoryId, function(err, category) {
                category.movies.push(_movie._id);
                category.save(function(err, category) {
                    res.redirect('/movie/' + movie._id);
                })
            })
        })
    }
}
```

这个时候，在 `db.movies` 中创建了含有 `category` 字段的一条数据，在 `db.categories` 中对应分类的 `movies` 数组中也添加了对该电影的引用。

我们可以修改 `/` 对应的页面，将电影按照分类来进行显示：

`index.jade`

```
extends ../layout

block content
    .container
        .row
            each cat in categories
                .panel.panel-primary
                    .panel-heading
                        h3 #{cat.name}
                    .panel-body
                        if cat.movies && cat.movies.length > 0
                            each item in cat.movies
                                .col-md-2
                                    .thumbnail
                                        a(href='/movie/#{item._id}')
                                            img(src='#{item.poster}', alt='#{item.title}')
                                        .caption
                                            h3 #{item.title}
                                            p: a.btn.btn-primary(href='/movie/#{item._id}', role='button')
                                                观看预告片
```

然后修改 `/` 对应的路由处理 `/app/controller/index.js`：

```
let Movie = require('../models/movie');
let Category = require('../models/category');

exports.index = function(req, res) {

    Category.find({})
    .populate({path: 'movies', options: {limit: 5}})
    .exec(function(err, categories) {
        if (err) {
            console.log(err);
        }
        res.render('index', {
            title: 'Shiningdan 首页',
            categories: categories,
        });
    });
}
```

当点击 `/admin/movie/list/` 页面中的更新按钮时，跳转的对象是不正确的，所以需要修改跳转的对象：

`list.jade`

```
td: a(target='_blank', href='/movie/#{item._id}') 查看
td: a(target='_blank', href='/admin/movie/update/#{item._id}') 修改
```

然后要修改 `/admin/movie/update/#{item._id}` 中的请求处理方法，在 `/app/controllers/movie.js` 中修改 `update` 方法：

```
exports.update = function(req, res) {
    let id = req.params.id;
    if (id) {
        Movie.findById(id, function(err, movie) {
            Category.find({}, function(err, categories) {
                res.render('admin', {
                    title: 'shiningdan 后台更新页面',
                    movie: movie,
                    categories: categories,
                })
            })
        })
    }
}
```

### jsonp 同步豆瓣数据

使用 Jsonp 同步豆瓣数据，可以在 `/admin/movie` 中添加 `input` ，获得影片的 id ，然后发送 Ajax 来获取数据。豆瓣有提供 [Movie API](https://developers.douban.com/wiki/?title=movie_v2)。

首先在 `admin.js` 中创建请求豆瓣 API 的 blur 事件：

```
$('#douban').blur(function(event) {
    let douban = $(this);
    let id = douban.val();

    if(id) {
        $.ajax({
            url: 'https://api.douban.com/v2/movie/subject/' + id,
            cache: true,
            type: 'get',
            dataType: `jsonp`,
            crossDomain: true,
            jsonp: 'callback',
            success: function(data) {
                $('#inputTitle').val(data.title);
                $('#inputDoctor').val(data.directors[0].name);
                $('#inputYear').val(data.year);
                $('#inputCountry').val(data.countries[0]);
                $('#inputSummary').val(data.summary);
                $('#inputPoster').val(data.images.large);
            },
        });
    }
});
```

然后在 `admin.jade` 中添加一个 input，输入需要同步的影片 id：

```
form.form-horizontal(method='post', action='/admin/movie/new')
    .form-group
        label.col-sm-2.control-label 豆瓣同步
        .col-sm-2
            input#douban.form-control(type='text')
    if movie._id
        input(type='hidden', name='movie[_id]', value=movie._id)
    .from-group
        label.col-sm-2.control-label(for='inputCategory') 电影分类
        .col-sm-10
            input#inputCategory.form-control(type='text', name='movie[categoryName]', value=movie.categoryName)    
```

并且在 `admin.jade` 的最后引入 `admin.js`:

```
script(src='/js/admin.js')
```

### 电影录入增加分类自定义

电影的分类不一定在 categories 里面都可以找到，所以在添加电影数据的时候，如果是不存在的电影分类，就创建一个新的分类：

```
exports.save = function(req, res) {
    let movieObj = req.body.movie;
    let id = movieObj._id;
    let _movie;
    if (id) {
        Movie.findById(id, function(err, movie) {
            if (err) {
                console.log(err);
            }
            _movie = underScore.extend(movie, movieObj);
            _movie.save(function(err, movie) {
                if (err) {
                    console.log(err);
                }
                res.redirect('/movie/' + movie._id);
            })
        })
    } else {
        _movie = Movie(movieObj);
        // _id 在调用 Movie() 的时候会自动生成
        let categoryId = movieObj.category;
        let categoryName = movieObj.categoryName;
        console.log(movieObj);
        _movie.save(function(err, movie) {
            if (err) {
                console.log(err);
            }

            if (categoryId) {
                Category.findById(categoryId, function(err, category) {
                    category.movies.push(_movie._id);
                    category.save(function(err, category) {
                        res.redirect('/movie/' + movie._id);
                    })
                })
            } else if(categoryName) {
                let category = new Category({
                    name: categoryName,
                    movies: [movie._id],
                });
                category.save(function(err, category) {
                    _movie.category = category._id;
                    _movie.save(function(err, movie) {
                        res.redirect('/movie/' + movie._id);
                    })
                })
            }
        });
    }
}
```

### 增加分类列表及分页

在首页，原有的展示页面是显示不同的分类，在每个分类下显示其中的电影。现在可以添加用户针对分类的查询，当点击分类的时候，可以导航到针对单个分类的查询结果上，所以，首先修改 `index.jade` 添加对分类的跳转：

```
each cat in categories
    .panel.panel-primary
        .panel-heading
            h3 
                a(href='/results?cat=#{cat._id}&p=0') #{cat.name}
        .panel-body
```

在 `route.js` 中添加对 `/result` URL 的跳转：

```
app.get('/results', Index.search);
```

创建一个新的 `reuslts.jade`，作为分类查找显示页面的模板：

```
extends ../layout

block content
    .container
        .row
            .panel.panel-default
                .panel-heading
                    h3 #{keyword}
                .panel-body
                    if movies && movies.length > 0
                        each item in movies
                            .col-md-2
                                .thumbnail
                                    a(href='/movie/#{item._id}')
                                        img(src='#{item.poster}', alt='#{item.title}')
                                    .caption
                                        h3 #{item.title}
                                        p: a.btn.btn-primary(href='/movie/#{item._id}', role='button')
                                            观看预告片
            ul.pagination
                - for (var i = 0; i < totalPage; i++) {
                    - if (currentPage == (i + 1)) {
                        li.active
                            span #{currentPage}
                    - } else {
                        li
                            a(href='/results?#{query}&p=#{i}') #{i+1}
                    - }
                - }
```

然后在 `/app/controllers/index.js` 中创建 `search` 方法来处理对 `/results?cat=#{cat._id}&p=0'` 的路由请求：

```
exports.search = function(req, res) {
    let catId = req.query.cat;
    let page = parseInt(req.query.p);
    let count = 2;
    let index = page * count;

    Category.find({_id: catId})
    .populate({
        path: 'movies',
        select: 'title poster',
    })
    .exec(function(err, categories) {
        if (err) {
            console.log(err);
        }
        let category = categories[0] || {};
        let movies = category.movies || [];
        let results = movies.slice(index, index + count);

        res.render('results', {
            title: 'Shiningdan 分类电影页面',
            keyword: category.name,
            currentPage: (page + 1),
            query: 'cat=' + catId,
            totalPage: Math.ceil(movies.length/count),
            movies: results,
        });
    })
}
```

### 增加搜索、公用列表及分页

在 `header.jade` 里面加入搜索框：

```
.container
    .row
        .page-header.clearfix
            h1 #{title}
            .col-sm-4
                small 重度科幻迷
            .col-sm-8
                form(method='GET', action='/results')
                    .input-group.col-sm-4.pull-right
                        input.form-control(type='text', name='q')
                        span.input-group-btn
                            button.btn.btn-default(type='submit') 搜索
```

然后该查询的目的地址是 `/result`，所以要在 `index.search` 函数中添加对应路径的处理：

```
exports.search = function(req, res) {
    let catId = req.query.cat;
    let q = req.query.q;
    let page = parseInt(req.query.p, 10) || 0;
    let count = 2;
    let index = page * count;

    if (catId) {
        Category.find({_id: catId})
        .populate({
            path: 'movies',
            select: 'title poster',
        })
        .exec(function(err, categories) {
            if (err) {
                console.log(err);
            }
            let category = categories[0] || {};
            let movies = category.movies || [];
            let results = movies.slice(index, index + count);

            res.render('results', {
                title: 'Shiningdan 分类电影页面',
                keyword: category.name,
                currentPage: (page + 1),
                query: 'cat=' + catId,
                totalPage: Math.ceil(movies.length/count),
                movies: results,
            });
        })
    } else {
        Movie.find({title: new RegExp(q+'.*', 'i')}, function(err, movies) {
            if (err) {
                console.log(err);
            }

            let results = movies.slice(index, index+count);
            res.render('results', {
                title: 'Shiningdan 分类电影页面',
                keyword: q,
                currentPage: (page + 1),
                query: 'cat=' + catId,
                totalPage: Math.ceil(movies.length/count),
                movies: results,
            });
        });
    }  
}
```

此时搜索 `欢乐` 就可以返回欢乐的搜索结果：

![](http://ojt6zsxg2.bkt.clouddn.com/5f17cd06906e86d42f4d3832665661ae.png)



