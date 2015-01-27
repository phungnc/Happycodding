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
$ yo angular
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

```
$ npm install yo yeoman-generator --save
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

At this point, you have a working generator. The next logical step would be to run it and see if it works.

"Since you're developing the generator locally, it's not yet available as a global npm module. A global module may be created and symlinked to a local one, using npm. Here's what you'll want to do:

On the command line, from the root of your generator project (in the generator-name/ folder), type:"

```
$ npm link
```

That will install your project dependencies and symlink a global module to your local file.
It mean that, you have installed `simple-yeoman` on the local. Now you can call

```
$ yo simple-yeoman
```
This will output log:

```
makeAppStructure method ran!
cloneTemplateFile method ran
```

#### Make more

- Make app structure

Open `index.js` and add Yeoman `mkdir` function.

```js
'use strict';
var generators = require('yeoman-generator');

module.exports = generators.Base.extend({
  constructor: function() {
    generators.Base.apply(this, arguments);
  },
  makeAppStructure: function() {
    console.log('makeAppStructure method ran!');
    // Create scaffolder
    this.dest.mkdir('src');
    this.dest.mkdir('src/styles');
    this.dest.mkdir('src/styles/base');
  },
  cloneTemplateFiles: function() {
    console.log('cloneTemplateFile method ran');
  }
});

```
Make project dir, get into it

```
$ mkdir simple-yeoman-demo
$ cd simple-yeoman-demo
```

Call simple-yeoman generator

```
$ yo simple-yeoman
```

This will create folder in simple-yeoman-demo project root.

```
└── src
  └── styles
    └── base
```

*Project root*:
While running a generator, Yeoman searches the directory tree for a `.yo-rc.json` file.
If found, it considers the location of the file as the root of the project.


For ex, if we have folder like:

```
parent-of-simple-yeoman-demo
  └── simple-yeoman-demo
  └── .yo-rc.json
```

Above `yo simple-yeoman` will create `src` directory at `parent-of-simple-yeoman-demo` not working directory `simple-yeoman-demo`, even you are stay in it.
So, if your generator is not running in your current working directory, make sure you don't have a `.yo-rc.json` somewhere up the directory tree.


- Clone template files to project

Yeoman will use the templates directory as the path for reading data and the folder the user is running your generator as the root path for outputting files.
We make templates directory as below:

```
├───package.json
├───app/
    └───index.js
├───templates/
    └───styles/base/_base.less
```

```js
'use strict';
var generators = require('yeoman-generator');

module.exports = generators.Base.extend({
  constructor: function() {
    generators.Base.apply(this, arguments);
  },
  makeAppStructure: function() {
    // Create scaffolder
    this.dest.mkdir('src');
    this.dest.mkdir('src/styles');
    this.dest.mkdir('src/styles/base');
  },
  cloneTemplateFiles: function() {
    // clone template file
    this.src.copy('styles/base/_base.less', 'src/styles/base/base.less')
  }
});

```

Output:

```
create src/styles/base/base.less
```

### Make complex `generator`

Yeoman team built a [generator-generator](https://github.com/yeoman/generator-generator) to help users get started with their own generator.

```
$ npm install -g generator-generator
```
Create the actual project, navigate to the folder of your choosing and run:

```
$ yo generator
```
After answer some question, we have structure like this:

![Generator Structure](https://raw.githubusercontent.com/phungnc/Happycodding/feature/yeoman/FrontEnd/Build%20Tools/generator-generator-structure.png)

From the skeleton of Generator, you can build Generator your self

Ref [this article](http://code.tutsplus.com/tutorials/build-your-own-yeoman-generator--cms-20040) to know how to build your Generator base one `generator-generator`

Happy Codding!
