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

To create your own yeoman generator, you should understand how Yeoman generator work

![Yeoman Generator](https://raw.githubusercontent.com/phungnc/Happycodding/feature/yeoman/FrontEnd/Build%20Tools/yeoman-generator.png)

Basically Yeoman generator will

1. Make app structure
2. Clone template files to project

As you see, the generator save time, and help team members follow code convention.

You can follow the article of Yeoman page to get more idea of Yeoman generator

http://yeoman.io/authoring/


### Make a simple Yeoman generator

#### Create project folder

```
$ mkdir simple-yeoman-generator
```
#### Init project

Yeoman is a Node.js module. We can use `npm init` to create a `package.json`
- The name property must be prefixed by `generator-`
- The keywords property must contain "yeoman-generator"
- The repo must have a description to be indexed by our [generators page](http://yeoman.io/generators)

```json
{
  "name": "generator-simple-yeoman",
  "version": "1.0.0",
  "description": "simple yeoman generator demo",
  "main": "index.js",
  "scripts": {
    "test": "test"
  },
  "keywords": [
    "yeoman-generator"
  ],
  "author": "phungnc@gmail.com",
  "license": "ISC",
  "dependencies": {
    "yeoman-generator": "^0.18.7"
  }
}
```

#### Install yeoman-generator

```js
npm install yo yeoman-generator --save
```

#### Create project tree

```
├───package.json
├───app/
    └───index.js
```

#### Write actual generator

index.js

```js
'use strict'
var generators = require('yeoman-generator');

module.exports = generators.Base.extend({
  constructor: function() {
    generators.Base.apply(this, arguments);
  },
  makeAppStructure: function() {
    console.log('makeAppStructure method ran!');
  },
  cloneTemplateFiles: function() {
    console.log('cloneTemplateFile method ran');
  }
});

```
Every method added to the prototype is run once the generator is called--and usually in sequence

#### Running the generator

"Since you're developing the generator locally, it's not yet available as a global npm module. A global module may be created and symlinked to a local one, using npm. Here's what you'll want to do:

On the command line, from the root of your generator project (in the generator-name/ folder), type:"

```
npm link
```

Run,

```
yo simple-yeoman
```

Output:

```
makeAppStructure method ran!
cloneTemplateFile method ran
```

#### Make more useful

- Make app structure

```js
'use strict';
var util = require('util');
var path = require('path');
var yeoman = require('yeoman-generator');

var simpleGen = yeoman.generators.Base.extend({
  constructor: function() {
    yeoman.generators.Base.apply(this, arguments);
  },
  makeAppStructure: function() {
    console.log('makeAppStructure method ran!');
    // Create scaffolder
    this.dest.mkdir('src');
    this.dest.mkdir('src/images');
    this.dest.mkdir('src/scripts');
    this.dest.mkdir('src/styles');
  }
  cloneTemplateFiles: function() {
    console.log('cloneTemplateFile method ran');
  }
});

module.exports = simpleGen;
```

- Clone template files to project

```js
'use strict';
var util = require('util');
var path = require('path');
var yeoman = require('yeoman-generator');

var simpleGen = yeoman.generators.Base.extend({
  constructor: function() {
    yeoman.generators.Base.apply(this, arguments);
  },
  makeAppStructure: function() {
    console.log('makeAppStructure method ran!');
    // Create scaffolder
    this.dest.mkdir('src');
    this.dest.mkdir('src/images');
    this.dest.mkdir('src/scripts');
    this.dest.mkdir('src/styles');
  }
  cloneTemplateFiles: function() {
    console.log('cloneTemplateFile method ran');
    this.src.copy('styles/base/base.less', 'src/styles/base/base.less');
  }
});

module.exports = simpleGen;
```

### More complex

You could use [generator-generator](https://github.com/yeoman/generator-generator)
to generate a Yeoman Generator.
