[![Neat](http://images.thoughtbot.com/bourbon/neat-logo.svg)](http://neat.bourbon.io)

*This is a port of https://github.com/lacroixdesign/node-neat updating to version 3.0.0 use at your own risk. I am not avail for help. I just needed an updated version.

*This is a node-sass port of the [Neat](http://neat.bourbon.io) library. If you
are looking for the original Ruby/Rails version, you can find it
[here](https://github.com/thoughtbot/neat).*

[![Build Status](http://img.shields.io/travis/lacroixdesign/node-neat.svg?style=flat)](https://travis-ci.org/lacroixdesign/node-neat)

# Contents

- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
  - [Basic Usage](#basic-usage)
  - [gulp.js](#gulpjs-usage)
  - [Grunt](#grunt-usage)
  - [node-sass](#node-sass-usage)
- [Getting Help](#getting-help)
- [Testing](#testing)
- [Credits](#credits)
- [License](#license)

# Requirements
- [node](http://nodejs.org)
- [gulp.js](http://gulpjs.com) -or- [Grunt](http://gruntjs.com) -or- [node-sass](https://github.com/andrew/node-sass)

# Installation

To install as a development dependency, run:

```bash
npm install --save-dev node-neat-2
```

If you need it in production, replace `--save-dev` with `--save`.

# Usage

## Basic Usage

To use `node-neat-2` with tools like [gulp.js](#gulpjs-usage), [Grunt](#grunt-usage), or directly with [node-sass](#node-sass-usage), provide the path to Neat in your Sass config. There are a couple of convenience methods for this, depending on whether you want Sass to include additional directories or not.

### with() Function

The `with()` function will include any additional paths you pass as arguments.

Returns an array of paths.

```javascript
var neat = require('node-neat-2');
// Any of these will return an array of Neat & Bourbon's paths plus your custom path(s)
neat.with('path/to/stylesheets')
neat.with('path/to/stylesheets1', 'path/to/stylesheets2')
neat.with(['path/to/stylesheets1', 'path/to/stylesheets2'])
```

### includePaths Property

The `includePaths` property returns an array of Neat & Bourbon's paths to use in your config.

```javascript
var neat = require('node-neat-2');
neat.includePaths // Array of Neat paths
```

### Stylesheet usage

Use either method above with the Sass config for your chosen tool (gulp.js, Grunt, etc.), then it's business as usual for Neat & Bourbon in your stylesheet:

```scss
@import "neat";
```

## gulp.js Usage

Using the [gulp-sass](https://github.com/dlmanning/gulp-sass) plugin.

```javascript
var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('sass', function () {
  gulp.src('path/to/input.scss')
    .pipe(sass({
      // includePaths: require('node-neat-2').with('other/path', 'another/path')
      // - or -
      includePaths: require('node-neat-2').includePaths
    }))
    .pipe(gulp.dest('path/to/output.css'));
});
```

## Grunt Usage

### Using *grunt-sass*

The [grunt-sass](https://github.com/sindresorhus/grunt-sass) task uses
[node-sass](https://github.com/andrew/node-sass)
([LibSass](https://github.com/hcatlin/libsass)) underneath, and is the recommended
way to use Grunt with node-neat-2.

Example config:

```javascript
grunt.initConfig({
  sass: {
    dist: {
      options: {
        // includePaths: require('node-neat-2').with('other/path', 'another/path')
        // - or -
        includePaths: require('node-neat-2').includePaths
      },
      files: {
        'path/to/output.css': 'path/to/input.scss'
      }
    }
  }
});
```

### Using *grunt-contrib-sass*

If you are using the Ruby version of Sass with node-neat-2, then you will need to use
the [grunt-contrib-sass](https://github.com/gruntjs/grunt-contrib-sass) task instead.

*Note that node-neat-2 is __NOT__ tested against the __Ruby__ version – only against __LibSass__.*

Example config:

```javascript
grunt.initConfig({
  sass: {
    dist: {
      options: {
        // loadPath: require('node-neat-2').with('other/path', 'another/path')
        // - or -
        loadPath: require('node-neat-2').includePaths
      },
      files: {
        'path/to/output.css': 'path/to/input.scss'
      }
    }
  }
});
```

## node-sass Usage

Using it directly with [node-sass](https://github.com/andrew/node-sass).

```javascript
var sass    = require('node-sass')
var neat = require('node-neat-2');

sass.render({
  file: './application.scss',
  success: function(css){
    console.log(css);
  },
  error: function(error) {
    console.log(error);
  },
  // includePaths: neat.with('other/path', 'another/path'),
  // - or -
  includePaths: neat.includePaths,
  outputStyle: 'compressed'
});
```

# Getting Help

Again this is not the original project so use at your own risk.

Below is the original project and maintainer.
Feel free to tweet me with questions [@iamlacroix](https://twitter.com/iamlacroix), or [open a ticket](https://github.com/lacroixdesign/node-neat/issues) on GitHub.

# Testing

`node-neat-2` is tested against the examples provided in the
[Neat documentation](http://neat.bourbon.io/docs). The tests check for compile
errors, so if a feature compiles but the expected output is incorrect, be sure
to [open a ticket](https://github.com/lacroixdesign/node-neat/issues).

Run the tests with:

```
make test
```

# Credits

Michael LaCroix's original port of this project is here [node-neat](https://github.com/lacroixdesign/node-neat)

This port of node-neat is maintained by Jarett Schadlich, credit goes to Michael LaCroix, however all credits for the Bourbon library go to [thoughtbot, inc](http://thoughtbot.com/community):

> ![thoughtbot](http://thoughtbot.com/images/tm/logo.png)
>
> Neat is maintained and funded by [thoughtbot, inc](http://thoughtbot.com/community). Tweet your questions or suggestions at [@kaishin](https://twitter.com/kaishin) and [@kylefiedler](https://twitter.com/kylefiedler).

# License
node-neat-2 is Copyright © 2018 Jarett Schadlich. It is free software, and may be redistributed under the terms specified in the LICENSE file.

node-neat is Copyright © 2013-2014 Michael LaCroix. It is free software, and may be redistributed under the terms specified in the LICENSE file.
