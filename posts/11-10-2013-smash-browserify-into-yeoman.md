# Smash Browserify into Yeoman

[Browserify](http://browserify.org/) is kind of awesome.

Coincidentally, [Yeoman](https://yeoman.io) is also kind of awesome.

Smashing them together turns out to be pretty easy, thanks to [grunt-browserify](https://github.com/jmreidy/grunt-browserify).

* The following is based on `generator-webapp` 0.4.4. Depending on the generator you used and its version, things might require more tweaking.

## Wire it up.

#### `Terminal`

```bash
$ npm install grunt-browserify --save-dev
```

#### `Gruntfile.js`

```js
grunt.initConfig({
    ...
    watch: {
        ...
        scripts: {
            files: [
                '<%= yeoman.app %>/scripts/**/*.js',
                '!<%= yeoman.app %>/scripts/main.compiled.js'
            ],
            tasks: ['browserify']
        }
        ...
    },
    ...
    browserify: {
        app: {
            files: {
                '<%= yeoman.app %>/scripts/main.compiled.js': [
                    '<%= yeoman.app %>/scripts/**/*.js',
                    '!<%= yeoman.app %>/scripts/main.compiled.js'
                ]
            }
        }
    },
    ...
    concurrent: {
        server: [
            ...
            'browserify'
        ]
        ...
    }
});
```

#### `app/index.html`

```html
    ...
    <!-- build:js scripts/main.js -->
    <script src="scripts/main.compiled.js"></script>
    <!-- endbuild -->
</body>
</html>
```

## Run the server.

#### `Terminal`

```bash
$ grunt serve
```

## Write node-y code.

#### `app/scripts/hi-from-stephen.js`

```js
module.exports = function () {
  return 'hi!';
};
```

#### `app/scripts/main.js`

```js
var hi = require('./hi-from-stephen');

console.log(hi()); // hi!
```

## Use npm-y code.

#### `Terminal`

```bash
$ npm install lodash --save
```

#### `app/scripts/main.js`

```js
var _ = require('lodash');

var happyLanguage = {
  'isn\'t': 'is',
  stinky: 'silly',
  monkeyhead: 'banana buddy'
};

var meanThings = 'browserify isn\'t special you stinky monkeyhead';

function replaceWord(word) {
  return happyLanguage[word] || word;
}

meanThings = _.map(meanThings.split(' '), replaceWord).join(' ');

document.body.innerHTML = meanThings;
```
