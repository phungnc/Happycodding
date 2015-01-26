## Jade

### Template

Jade is template engine. Jade can output HTML dynamically with Javascript variable.

Example

We have Javascript object as bellow:

```json
{
  "package" : {
    "title": "Aris VietNam",
    "description": "This is home page of Aris Vietnam",
    "keywords": [
      "Aris",
      "VietNam",
      "IT",
      "Outsource"
    ],
    "robots": [
      "INDEX",
      "FOLLOW",
      "NOODP",
      "NOYDIR",
      "NOARCHIVE"
    ]
  }
}
```
We can write Jade template to transfer `package` object to Jade.

```html
doctype html
html
  head
    meta(charset='UTF-8')
    title= package.title
    meta(name='description', content=package.description)
    meta(name='keywords', keywords=package.keywords)
    meta(name='robots', keywords=package.robots)
  body
    h1= package.title
    p Welcome to #{package.title} !
```

Explain

- title= package.title:

	This will get data `package.title` for `title` element.

- content= package.description

	This will get data `package.descripttion` for `content` element.

- the same for other elements: `keywords`, `robots`, `content`.

The output HTML will be:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Aris VietNam</title>
    <meta name="description" content="This is home page of Aris Vietnam">
    <meta name="keywords" keywords="Aris,VietNam,IT,Outsource">
    <meta name="robots" keywords="INDEX,FOLLOW,NOODP,NOYDIR,NOARCHIVE">
  </head>
  <body>
    <h1>Aris VietNam</h1>
    <p>Welcome to Aris VietNam !</p>
  </body>
</html>
```

Get hands dirty
(Require read [[gulp| Gulp Article]])

Using `gulp` to generate above HTML step by step

1. Create project folder:

2. Use command line, go into that project

3. Init nodejs project command: `npm init`

4. Install packages: `npm install gulp gulp-jade gulp-data --save-dev`

5. Create `gulpfile.js`

6. Run task `templates` to generate HTML

gulpfile.js

```js
var gulp, jade, data, path;

gulp = require('gulp');
jade = require('gulp-jade');
data = require('gulp-data');
path = require('path');

/* get Json data callback function */
var getJsonData = function(file, callback) {
	var jsonPath = './config.json';
	callback(undefined,	require(jsonPath));
};

gulp.task('templates', function(){
	gulp.src('./jade/*.jade')
	.pipe(data(getJsonData))
	.pipe(jade({
		pretty: true
	}))
	.pipe(gulp.dest('./dist/'));
});
```
### Component

The good part of Jade.

We will make a simple page.

![image](https://192.168.1.202/attachments/download/719/jade-layout.png)

Now, let devide it into components.

![image](https://192.168.1.202/attachments/download/720/jade-component.png)

#### Get dirty hand

Create jade-component folder to content .jade files

_layout.jade

```jade
doctype
html
  head
    title My Site
    link(rel='stylesheet', href='../stylesheets/style.css')
  body
    header
      include _header
    .container
      .main-content
        block content
      .sidebar
        block sidebar
    footer
      include _footer
```

index.jade

```jade
extend _layout
block content
  include _inc_content
block sidebar
  include _inc_widget
```

_header.jade

```jade
h1 Header partial
```

_footer.jade

```jade
p
  | Footer partial
p
  | phung.nc@aris-vn.com
```

_inc_content.jade

```jade
h1 Content
p
  | Jade is a terse language for writing HTML templates.
  | Produces HTML
  | Supports dynamic code
  | Supports reusability (DRY)
p
  | To read about the features of the language,
  | select them from the navigation menu on the right.
  | To read about the features of the language,
  | select them from the navigation menu on the right.
  | To read about the features of the language,
  | select them from the navigation menu on the right.
```

_inc_widget.jade

```jade
.widget
  h1 Widget
  p
    | attribute: Tag attributes look similar to html
  p
    | case: The case statement is a shorthand for JavaScript's 'switch'
  p
    | code: Jade makes it possible to write inline JavaScript code in your templates.
  p
    | conditionals: Jade's first-class conditional syntax allows for optional parenthesis.
```

use gulp-jade to build generate HTML

Update gulpfile.js

```js
var gulp, jade, data, path;

gulp = require('gulp');
jade = require('gulp-jade');
data = require('gulp-data');
path = require('path');

/* get Json data callback function */
var getJsonData = function(file, callback) {
	var jsonPath = './config.json';
	callback(undefined,	require(jsonPath));
};

gulp.task('templates', function(){
	gulp.src('./jade/*.jade')
	.pipe(data(getJsonData))
	.pipe(jade({
		pretty: true
	}))
	.pipe(gulp.dest('./dist/'));
});

gulp.task('component', function(){
	gulp.src('./jade-component/index.jade')
	.pipe(jade({
		pretty: true
	}))
	.pipe(gulp.dest('./dist-component/'));
});
```

```
gulp component
```

TODO

#### extends, block, include  

##### extends

##### block

##### include

### Repository

https://192.168.1.202/git/web.gulp.jade
