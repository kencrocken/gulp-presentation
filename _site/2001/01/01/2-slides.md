## The Repetitive Task
- Compiling SASS/LESS to CSS <!-- .element: class="fragment" -->
- Minifying <!-- .element: class="fragment" -->
- Bundling <!-- .element: class="fragment" -->
- Linting <!-- .element: class="fragment" -->
- Copying files <!-- .element: class="fragment" -->
- Refereshing the browser(s) <!-- .element: class="fragment" -->

---

[gulpLog]: /images/gulp-log.png "Gulp log"
##AUTOMATE!
![Alt text][gulpLog]

---

## What is Gulp?
- Gulp is a javascript task/build runner allowing for the automation of tasks  <!-- .element: class="fragment" -->

--

### Gulp workflow
- Define a task <!-- .element: class="fragment" -->
- Load a set of files in the gulp task stream to be processed. <!-- .element: class="fragment" -->
- Modify the files in the stream.<!-- .element: class="fragment" -->
- Send the new files to a specified destination. <!-- .element: class="fragment" -->

--

### Gulp API 
- `gulp.task` defines the task.
- `gulp.src` Emits files matching provided pattern, returning a stream of vinyl files that can be piped.
- `gulp.dest` Can be piped to and it will write files.
- `gulp.watch` Watch files and do something when a file changes.

[gulp api docs](https://github.com/gulpjs/gulp/blob/master/docs/API.md)

--

### Example Task
```js
// Install the relevant modules
// npm i --save-dev gulp gulp-sass gulp-sourcemaps gulp-autoprefixer

'use strict';

var gulp = require('gulp');
var sass = require('gulp-sass');
var sourcemaps = require('gulp-sourcemaps');
var autoprefixer = require('gulp-autoprefixer');

gulp.task('sass', function() {
  return gulp.src('sass/main.scss')
    .pipe(sourcemaps.init())
    .pipe(sass({
      outputStyle: 'nested',
      includePaths: [
        "bower_components/susy/sass"  
      ]
    }))
    .pipe(autoprefixer('last 2 versions', '> 1%', 'ie 9'))
    .pipe(sourcemaps.write('.'))
    .pipe(gulp.dest('dist/styles/'));
});
```

--

### Gulp CLI 

`gulp <task> <othertask>`

Just running `gulp` will execute the task you defined as `default`. If there is no `default` task gulp will error.

`gulp -T`  returns a task dependency tree for the loaded gulpfile.

[gulp cli docs](https://github.com/gulpjs/gulp/blob/master/docs/CLI.md)

--

### gulpfile.babel.js, ES6 

`npm i --save-dev babel-core babel-preset-es2015`

- Rename gulpfile.js to gulpfile.babel.js  

--

### Example task in ES6

```js
'use strict';

import sass         from 'gulp-sass';
import sourcemaps   from 'gulp-sourcemaps';
import autoprefixer from 'gulp-autoprefixer';

gulp.task('sass', ()=> {
  return gulp.src('sass/main.scss')
    .pipe(sourcemaps.init())
    .pipe(sass({
      outputStyle: 'nested',
      includePaths: [
        "bower_components/susy/sass"  
      ]
    }))
    .pipe(autoprefixer('last 2 versions', '> 1%', 'ie 9'))
    .pipe(sourcemaps.write('.'))
    .pipe(gulp.dest('dist/styles/'));
});
```

--

### Gulpfile Organization

- Gulp files with minimal tasks, ok to keep it in one file.
- Gulp files can get long, might be best to break it up into multiple files
- Mindful of task dependencies.  Below the default tasks only run after the 'hello' and 'sass' tasks complete.  

```js
gulp.task('default', ['hello', 'sass'], function() {
    console.log("DEFAULT TASK");
});
```

---

## Fini
### Sources
[What is gulp.js?](http://brandonclapp.com/what-is-gulp-js-and-why-use-it/)  
[Automating Build Tasks With Gulp](http://www.danielgynn.com/automating-build-tasks-with-gulp/)  
[Using ES6 with Gulp](https://markgoodyear.com/2015/06/using-es6-with-gulp/)  
[ES6 Features](http://es6-features.org)  
[Import/Modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)  
[Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)  
[Template Strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)  
[Constants](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)  