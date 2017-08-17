### 1. npm-npmscript-gulp-webpack

```
npm install -g <module name>
```

### 2. package.json 有什么作用？

每个项目下基本都会有一个package.json文件，这个文件相当于本地项目的一个说明（项目名、版本号、描述、作者等信息），它允许你指定项目中所使用的依赖。npm install命令会根据这个配置文件，自动下载所需依赖，也就是配置项目所需的运行和开发环境。

可以通过 npm init 来创建一个package.json

```
{
  "name": "blog",  //项目名称
  "version": "1.0.0",  //版本号
  "description": "my blog",  //描述
  "main": "index.js",  //入口
  "scripts": {  //执行命令行
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [  //关键字
    "blog"
  ],
  "author": "RobbChan",  //作者
  "license": "MIT",  //许可证
  "dependencies": {  //生产环境依赖
    "express": "^4.15.2"
  },
  "devDependencies": {  //开发环境依赖
    "coffee-script": "~1.6.3"
  }
}
```

### 3. npm install --save app 与 npm install --save-dev app有什么区别?

- --save 将项目所需要的依赖的模块信息添加到package.json的dependencies中，上线后仍需要使用
- --save-dev 将项目的开发环境需要的依赖模块添加到到package.json的devDependencies中,只有在开发时才用到

### 4. node_modules的查找路径是怎样的?

从当前文件目录开始查找node_modules，然后依次进入父目录，查找父目录下的node_modules，依次向上查找，直到根目录的node_modules。如某个模块的绝对路径为/user/src/app.js，在该模块中使用require('mo'),则node的查找路径如下：

/user/src/node_modules/mo ==>  /user/node_modules/mo ==> /node_modules/mo

### 6.  webpack是什么？和其他同类型工具比有什么优势？

> Webpack 是当下最热门的前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载。通过 loader 的转换，任何形式的资源都可以视作模块，比如 CommonJs 模块、 AMD 模块、 ES6 模块、CSS、图片、 JSON、Coffeescript、 LESS 等。

- webpack是以commonJS的形式来书写脚本，但对AMD/CMD的支持也很全面
- webpack可以将代码拆分为多个区块，每个区块包含一个或多个模块，它们可以按需异步加载，极大地减少了页面初次加载时间
- webpack本身只能处理原生JS模块，但是loader转换器可以将各种类型的资源转换成JS模块。这样，任何资源都可以成为webpack可以处理的模块
- webpack有一个智能解析器，几乎可以处理任何第三方库，无论它们的模块形式是commonJS,AMD还是普通的JS文件。
- webpack还有一个功能丰富的插件系统。大多数内容功能都是基于这个插件系统运行的，还可以开发和使用开源的webpack插件，来满足各种各样的需求。
- webpack使用异步I/O和多级缓存提高运行效率，使得它能够快速增量编译。

### 7. npm script是什么？如何使用？

package.json文件有一个scripts字段，可以用于指定脚本命令，供npm直接调用。

```
"scripts": { 
    "start": "echo here we go",
    "test": "echo \"Error: no test specified\" && exit 1",
    "say": "echo say1"
  }
```

如上，通过 npm run <字段名>  来调用, 由于npm内置了start和test命令，可以直接通过 npm start 和 npm test 直接调用

### 8. 使用 webpack 替换 入门-任务15中模块化使用的 requriejs

[项目预览](https://kmac007.github.io/demos/webpack-demo/index.html)

[代码](https://github.com/kmac007/demos/tree/master/webpack-demo)

### 9. gulp是什么？使用 gulp 实现图片压缩、CSS 压缩合并、JS 压缩合并

gulp是前端开发过程中对代码进行自动化构建的工具。它不仅能对资源进行优化，而且在开发过程中能够通过配置，自动完成很多重复的任务，让我们可以更专注于代码，提高工作效率。我们可以用gulp：
1. 编译sass
2. 合并优化压缩css
3. 校验压缩js
4. 优化图片
5. 添加文件指纹(md5)
6. 实时自动刷新

```
//安装插件
npm install gulp-imagemin --save-dev //图片压缩
npm install gulp-cssnano --save-dev //css压缩
npm install uglify --save-dev //js压缩
npm install gulp-jshint --save-dev //js规范检查
npm install gulp-concat --save-dev　//文件合并
npm install gulp-rename --save-dev //重命名

//gulpfile.js
//引入插件
var gulp = require('gulp'),
  cssnano = require('gulp-cssnano'),
  concat = require('gulp-concat'),
  jshint = require('gulp-jshint'),
  uglify = require('gulp-uglify'),
  imagemin = require('gulp-imagemin'),
  rename = require('gulp-rename');

//css合并压缩
gulp.task('build:css', function () {
  gulp.src('./src/css/*.css')
    .pipe(concat('merge.css')) //将文件合并
    .pipe(rename({
      suffix: '.min' //文件名后加上　.min 
    }))
    .pipe(cssnano()) //css压缩
    .pipe(gulp.dest('dist/css/')); //输出
})

//js合并压缩
gulp.task('build:js', function () {
  gulp.src('src/js/*.js')
    .pipe(jshint()) //js规范检查
    .pipe(jshint.reporter('default'))
    .pipe(concat('merge.js'))
    .pipe(rename({
      suffix: '.min'
    }))
    .pipe(uglify())
    .pipe(gulp.dest('dist/js/'));
})

//图片压缩
gulp.task('build:image', function () {
  gulp.src('src/imgs/*')
    .pipe(imagemin())
    .pipe(gulp.dest('dist/imgs/'));
})

gulp.task('build', ['build:css', 'build:js', 'build:image'])
```