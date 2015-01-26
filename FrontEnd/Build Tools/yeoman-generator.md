# Yeoman Generator

```js
_-----_
|       |
|--(o)--|   .--------------------------.
`---------´ |    Welcome to Yeoman,    |
( _´U`_ )   |   ladies and gentlemen!  |
/___A___\   '__________________________'
|  ~  |
__'.___.'__
´   `  |° ´ Y `
```

## About Yeoman

Yeoman page: http://yeoman.io/

THE WEB'S SCAFFOLDING TOOL FOR MODERN WEBAPPS

Basically Yeoman combine 3 tools in himself.

1. The scaffolding tool: [Yo](http://yeoman.io/)
2. The build tool: [Gulp](http://gulpjs.com/), [Grunt](http://gruntjs.com/), ...
3. The package manager: [Bower](http://bower.io/), [npm](https://www.npmjs.com/)

Yeoman workflow

![Yeoman workflow](https://raw.githubusercontent.com/phungnc/Happycodding/feature/yeoman/FrontEnd/Build%20Tools/yeoman-workflow.jpg)

## Install Yeoman

```js
npm install -g yo gulp bower
```

(I use gulp here because gulp is easer to start than grunt, for me)

## Use yeoman-generator to scaffolding project

Yeoman and community had create over 1000 generators

http://yeoman.io/generators/

You can use one of them to scaffolding the project

for ex.

```
yo angular
```

to scaffolding AngularJS project

## Create your own yeoman generator

### What is generator

![]()

### A Very simple

http://yeoman.io/authoring/

### More complex

You could use [generator-generator](https://github.com/yeoman/generator-generator)
to generate a Yeoman Generator.
