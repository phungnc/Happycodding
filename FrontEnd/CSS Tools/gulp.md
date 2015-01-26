## Gulp

"gulp's use of streams and code-over-configuration makes for a simpler and more intuitive build."

 - [Homepage](http://gulpjs.com)

### Gulp task flow

1. gulp.src(): create stream file
2. streaming plugin
3. gulp.dest(): save streaming file


_Note_: In stream, each file is one object


`htdocs/css/**/*.css`


have 3 files, then

```
gulp.src('htdocs/css/**/*.css')
```

will return 3 stream file objects

So, gulp can deal with multi files
-------

### Install gulp

#### 1. Install node.js

#### 2. Install gulp.js
##### 2.1. Install gulp globally:
```
$ npm install --global gulp
```
#### 2.2. Install gulp in your project devDependencies:
```
$ npm install --save-dev gulp
```
-------
### Use gulp

#### 1. Create project folder
```
mkdir path/to/project
cd path/to/project
```
#### 2. Create package.json (project profile)
```
npm init
```
* You can choose 'yes' to pass
Then, you will have package.json like below

```json
{
  "name": "demo02",
  "version": "1.0.0",
  "description": "demo for gulp",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
}
```
#### 3. Install gulp module

##### 3.1. Create gulpfile.js for Hello World :)

```js
var gulp;
	gulp = require('gulp');

gulp.task('default', function(){
	console.log('Hello World');
});
```
Then in command line, run

```js
gulp
```

You will see output

```
[10:17:12] Using gulpfile ~/workspace/lab/js/gulp/demo02/gulpfile.js
[10:17:12] Starting 'default'...
Hello World
[10:17:12] Finished 'default' after 136 μs
```

##### 3.2. Try some gulp module for project.

In this example, we will demo some gulp module:
 gulp-less
 gulp-connect

##### 3.2.1. gulp-less

```js
npm install gulp-less --save-dev
```

Then you will see package.json is updated

```json
{
  "name": "demo02",
  "version": "1.0.0",
  "description": "demo for gulp",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "gulp-less": "^1.3.6"
  }
}
```
Update gulpfile.js for less task

```js
var gulp, less;
	gulp = require('gulp');
	less = require('gulp-less');

gulp.task('default', function(){
	console.log('Hello World');
});

gulp.task('less', function(){
	gulp.src('./less/*.less')
	.pipe(less())
	.pipe(gulp.dest('./css'));

});
```

Create .less file

```css
html {
    background: #F6F7EF;
}
body {
    font-size: 15px;
    width: 900px;
    margin: 0 auto;
    background: #fff;
}
h1 {
    font-size: 20px;
}
.box {
    color: #ccc;
    overflow: hidden;
    div {
        float: left;
        text-align: center;
        width: 30%;
        height: 230px;
        line-height: 230px;
        margin-left: 22px;
        background: #eae;
    }
    p {
        margin: 10px;
        a {
            display: block;
            width: 120px;
            margin: 0 auto;
        }
    }
}
```
Then run

```
gulp less
```

You will see new css/style.css is created

Create index.html file to test

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Gulp sample</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <h1>Gulp sample</h1>
    <div class="box">
        <div>Box 1</div>
        <div>Box 2</div>
        <div>Box 3</div>
    </div>
</body>
</html>
```

Open file index.html in browser to see the result

##### 3.2.2. gulp-connect

[gulp-connect](https://www.npmjs.org/package/gulp-connect)

```js
npm install gulp-connect --save-dev
```
package.json is updated

```json
{
  "name": "demo02",
  "version": "1.0.0",
  "description": "demo for gulp",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "gulp-connect": "^2.0.6",
    "gulp-less": "^1.3.6"
  }
}
```
Update gulpfile.js for connect task

```js
var gulp, less, connect;
	gulp = require('gulp');
	less = require('gulp-less');
	connect = require('gulp-connect')


gulp.task('default', function(){
	console.log('Hello World');
});

gulp.task('less', function(){
	gulp.src('./less/*.less')
	.pipe(less())
	.pipe(gulp.dest('./css'));

});

gulp.task('connectDev', function(){
        connect.server({
                root: ['./'],
                port: 8000,
                livereload: true
        });
});

```
Then in command line

```js
gulp connectDev
```
This will create app server at

```
http://localhost:8000/
```
You can access this server to see page index

To usage liveReload, we will create task html, watch and livereload in gulpfile.js

```js
var gulp, less, connect;
	gulp = require('gulp');
	less = require('gulp-less');
	connect = require('gulp-connect')


gulp.task('default', function(){
	console.log('Hello World');
});

gulp.task('less', function(){
	gulp.src('./less/*.less')
	.pipe(less())
	.pipe(gulp.dest('./css'));

});

gulp.task('connectDev', function(){
        connect.server({
                root: ['./'],
                port: 8000,
                livereload: true
        });
});

gulp.task('html', function(){
        gulp.src('./*.html')
                .pipe(connect.reload());
});

gulp.task('watch', function(){
        gulp.watch(['./*.html'], ['html']);
        gulp.watch(['./less/*.less'], ['less']);
        gulp.watch(['./css/*.css'], ['html']);
});

gulp.task('livereload', ['watch', 'connectDev']);
```

Then in command line, run

```js
gulp livereload
```

Now if you change anything in less, css or html file this will reflect right away on browser.
