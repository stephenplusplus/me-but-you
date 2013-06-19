# Building Apps With The Yeoman Workflow

## What is Yeoman?

Trick question. It's not a thing. It's this guy:

** image **

Basically, he wears a top hat, lives in your computer, and waits for you to tell him what kind of application you wish to create. As an example, scaffolding a web application would look something like this:

```
$ yo webapp

     _-----_
    |       |
    |--(o)--|   .--------------------------.
   `---------´  |    Welcome to Yeoman,    |
    ( _´U`_ )   |   ladies and gentlemen!  |
    /___A___\   '__________________________'
     |  ~  |
   __'.___.'__
 ´   `  |° ´ Y `

Out of the box I include HTML5 Boilerplate, jQuery and Modernizr.
[?] Would you like to include Twitter Bootstrap for Sass?: (Y/n)
[?] Would you like to include RequireJS (for AMD support)?: (Y/n)
```

The first thing that comes to mind is OMG so dreamy. Second, thanks, bro.

All we did was tell him what we wanted and he replied with specific questions to give us even more control.

Let's go back a step, though. Not every new computer comes with a Yeoman pre-installed. He lives in the NPM package repository. You only have to ask for him once, then he packs up and moves into your hard drive. _Make sure you clean up, he likes new and shiny things._

He's a person with feelings and opinions, but he's very easy to work with. If you think he's too opinionated, he can be easily convinced.

Let's take a second to break apart what that `yo webapp` command really did.

### `yo`
This is an OS X, Linux, and Windows friendly system-wide command that scours your hard drive for any installed "generators," then gives them control based on the next argument:

### `webapp`
This is actually a separate plug-in, or "generator," called `generator-webapp`. Yeoman recognizes other `generator-____` Node modules, which opens the door for using Backbone, AngularJS, and countless other you-name-it generators.

Something important to take away from this is it's the `generator-webapp` module that prompts us with questions. The same goes for any other generators we install. They are maintained by the community, not necessarily the Yeoman team members themselves.

By using Yeoman, you're not saying "I want to do things your way, master. *bow* *bow*," without having any control. It's actually quite the opposite. What you're really saying is, "I want to make an application that follows best practices that have been discovered by frequent users and contributors of the web development community."

Seriously, you have to say it just like that, or it won't work.

Should you prefer to do something differently than what he gives you, you simply change the code that was generated for you, or even go to the source of the "generator" itself, and send in your contribution.


## Friendship

Our buddy, yo has some buddies of his own, and thinks you'll all get along over endless tea and smiles. If you haven't heard of [Grunt](http://gruntjs.com) or [Bower](http://bower.io), here's a quick summary of what these give us:

### Grunt
Grunt is a JavaScript-based task runner, that does the dirty stuff. Like `yo`, it also provides a base set of functionality, then allows the community to share their own plug-ins, or "tasks" that help accomplish common things. When you scaffold your application with `yo webapp`, Grunt and some hand-picked tasks will come along, which accomplish things like running your website in a local development environment, concatenating and minifying your code, optimizing your images, and much more. Tasks are run through the command line, by typing `grunt server`, `grunt build`, `grunt test`, and many more.

Tasks are defined and customized in a `Gruntfile.js` file, which lives in the root directory of your project. Check it out to see what Yeoman set up for you.

### Bower
Nobody likes going to GitHub or random developers' sites to download a .zip of a JavaScript tool. Like when fetching a Node package with `npm install ___`, Bower lets you say `bower install ___`. The component is then saved in a directory of your choosing, generally, `app/bower_components/` for Yeoman-generated apps. Assuming you wanted jQuery, you would run the `bower install query` command, then include the relevant file inside of your HTML file. In our case, `<script src="bower_components/jquery/jquery.js"></script>`


## A Typical Application

Let's get wild. It's time to create an app.

Real quick though, find your nearest terminal and make sure you have these things installed:

`$ npm install -g yo grunt-cli bower`

Since Yeoman is all about creating production-ready applications, he encourages testing with the help of [mocha](http://visionmedia.github.io/mocha/).

Create a folder we can play around in, then run:

```js
$ yo webapp
```

*So we're both looking at the same thing, answer `No` to any prompts that come up.

Here's what should have happened:

- A whole buncha stuff.

Did it? Good!

To prevent you from scrolling up through all of the text that was just spit out at you, here's an overview:

- The application was scaffolded:
```
create Gruntfile.js
create package.json
create .gitignore
create .gitattributes
create .bowerrc
create bower.json
create .jshintrc
create .editorconfig
create app/favicon.ico
create app/404.html
create app/robots.txt
create app/.htaccess
create app/styles/main.css
create app/index.html
create app/scripts/main.js
create app/scripts/hello.coffee
invoke   mocha:app
create     test/bower.json
create     test/.bowerrc
create     test/spec/test.js
create     test/index.html
```
- Your Bower components and NPM packages were installed:
```
I'm all done. Running bower install & npm install for you to install the required dependencies. If this fails, try running the command yourself.
```

Open the new stuff in your favorite editor, and we'll look over what we have.

```
├─ app/
│  ├─ images/
│  ├─ scripts/
│  │  ├─ hello.coffee
│  │  └─ main.js
│  ├─ styles/
│  │  └─ main.css
│  ├─ .htaccess
│  ├─ 404.html
│  ├─ favicon.ico
│  ├─ index.html
│  └─ robots.txt
│
├─ node_modules/
│  ├─ so/
│  ├─ many/
│  └─ packages/
│
├─ test/
│  ├─ spec/
│  │  └─ test.js
│  ├─ .bowerrc
│  ├─ bower.json
│  └─ index.html
│
├─ .bowerrc
├─ .editorconfig
├─ .gitattributes
├─ .gitignore
├─ .jshintrc
├─ bower.json
├─ Gruntfile.js
└─ package.json
```

If you take anything away from this article, let it be the beautiful file/folder text representation above. That just took a whole Mountain Dew of my time.

Back on track. What you're looking at is the most common application structure a Yeoman generator will produce.

`app/` is where your pure, non-compiled, non-minified source code lives.

`app/scripts/` is where your JavaScript goes. You're free to create sub-directories and even use CoffeeScript if that's your cup of tea. That didn't make sense. Again. You're free to use TeaScript if that's your cup of coffee. Nope.

`app/styles/` is where your CSS goes. Again, sub-directories, LESS, Sass, whatevs.

`app/index.html` is the non-minified version of `index.html` that will eventually be squashed and delivered to the client. More on that later.

`Gruntfile.js` has all of the build, server, and test tasks defined.

At this point, `yo` has done his job. He's given you everything you need to launch a production-ready web application. Let's now shift our focus to what Grunt tasks he's pre-configured for us.

### `grunt build`

Running `grunt build` takes your `app/` source code files and turns them into a distributable application, which ends up in `dist/`.

That `dist/` folder is what you feed to your server. `dist/` will have it's own `index.html`, with references to minified and concatenated `dist/scripts` and `dist/styles`, and optimized `dist/images`. Your users will appreciate this. Your phone-card, dial-up users will __really__ appreciate this.

Behind the scenes, `grunt build` is a task that runs several sub-tasks. One of those is [`grunt-usemin`](https://github.com/yeoman/grunt-usemin), which looks for blocks inside of your `app/index.html`, like this:

`app/index.html`
```
<!-- build:js scripts/main.js -->
<script src="bower_components/jquery/jquery.js"></script>
<script src="scripts/main.js"></script>
<!-- endbuild -->
```

After your `grunt build` task completes, you will end up with this:

`dist/index.html`
```
<script src="scripts/c155266f.main.js"></script>
```

It sucked those scripts up, concatenated, minified, and versioned them. Quite powerful.

That's one of the shining features about using Yeoman. Instead of manually defining what you want your build process to do each time you create an application, you can just place some trust in Yo and your chosen generator. Together, they'll wire you up with everything you need to launch a production-ready application.

### `grunt server`

Now that you've seen what type of work `grunt build` will do when your application is complete, you should probably start working on your application! We'll create one together in just a sec, but first let's see what kind of workflow we'll have. Like `grunt build`, `grunt server` uses several other Grunt tasks to make development as easy as it can be.

Try it out:

```
$ grunt server
Running "server" task

Running "clean:server" (clean) task
Cleaning ".tmp"...OK

Running "concurrent:server" (concurrent) task

    Running "coffee:dist" (coffee) task
    File .tmp/scripts/hello.js created.

    Done, without errors.

    Running "compass:server" (compass) task

    Done, without errors.

Running "connect:livereload" (connect) task
Starting connect web server on localhost:9000.

Running "open:server" (open) task

Running "watch" task
Waiting...
```

The aforementioned "several other Grunt tasks" are:

`clean:` Yeoman stores some stuff in a `.tmp` folder. That will be wiped out.

`coffee:` Compiles your CoffeeScript files from `app/scripts`.

`compass:` Compiles your Sass files from `app/styles`.

`connect:` Creates a local server, watches for changes to your source files, then triggers a reload in your browser.

`open:` Opens the server instance, typically `localhost:9000` in your browser

Make an edit or two in the source files to see the change reflected in the browser. Like I said above, this is about as easy as it can be. It just works.


## Let's App It Up!

I of course meant appetizers. Grab some cheese sticks, then meet me in a little bit.

*Wash your hands!*


## Let's Create an Application

To get a feel for some other Yeoman generators, let's try out Backbone. We'll create a simple To-Do app, use Bower for our dependencies, and even write a test.

```
$ Sound good? (Y/n)
```

I'll assume you entered "Y". We ride! But first:

```
# install the Backbone generator:
$ npm install -g generator-backbone

# make another play directory, then do these things:
$ yo backbone

     _-----_
    |       |
    |--(o)--|   .--------------------------.
   `---------´  |    Welcome to Yeoman,    |
    ( _´U`_ )   |   ladies and gentlemen!  |
    /___A___\   '__________________________'
     |  ~  |
   __'.___.'__
 ´   `  |° ´ Y `

Out of the box I include HTML5 Boilerplate, jQuery, Backbone.js and Modernizr.

Would you like to include Twitter Bootstrap for Sass? (Y/n) Y

Would you like to include RequireJS (for AMD support)? (Y/n) n
```

Open the new app in your editor. Things should feel quite familiar after our experience with the web app generator. You still have an `app` directory, with `scripts/`, `styles/` and an `index.html`.

Before we start editing files, run:

```
$ grunt server
```

As we talked about earlier, this starts the server, sets up watches on our files, blah blah yipsie-doodle. Your browser should open, and you should be greeted with an accent:

### 'Allo, 'Allo!

Well, shoot, we have to keep that. It's just so nice. However, let's clear out the other stuff.

`index.html`
```html
<div class="container">
    <div class="hero-unit">
        <h1>'Allo, 'Allo!</h1>
        <section id="todo-app">
            <!-- Where our To Do app will go -->
        </section>
    </div>
</div>
```

When you save, your browser will refresh, and there we have it! Just a simple, warm "'Allo, 'Allo".

Let's get ourselves a game plan. We know we're going to create a To Do app, but what might that look like? Will we need any other libraries to help us?

Hmm.

It's been at least 4 seconds, and I haven't heard any answers.

Alright, I'm gonna grab another Dew after that file tree drank my last one. I'll let you know if I think of anything.


## To Do: Set Up Our File Structure

B3. A terrible slot in a vending machine for a carbonated drink. Fizz, foam, disaster.

While I was in the bathroom washing my hands, I had a vision.

```
[ Add a New To Do ] ← input

checkbox
- clicking with draw a line through the title of the todo item
 ↓
[x] To Do Item #1
[ ] To Do Item #2
    ↑ title
      - double clicking will trigger an "edit" mode
```

Let's set ourselves up with a structure that will bring this vision to life. `generator-backbone`, came with some secret weapons: sub-generators. `yo backbone` scaffolded our application, but flip back to your terminal and check out what these guys can do:

```
# create a collection for our To Do items.
$ yo backbone:collection todos
    create app/scripts/collections/todos-collection.js

# create a model for a To Do item.
$ yo backbone:model todo
    create app/scripts/models/todo-model.js

# create a view for our list of To Do items.
$ yo backbone:view todos
   create app/scripts/templates/todos.ejs
   create app/scripts/views/todos-view.js

# create a view for just one To Do item.
$ yo backbone:view todo
   create app/scripts/templates/todo.ejs
   create app/scripts/views/todo-view.js
```

Check out your index.html:

```html
<!-- build:js scripts/main.js -->
<script src="scripts/main.js"></script>
<script src="scripts/templates.js"></script>
<script src="scripts/collections/todos-collection.js"></script>
<script src="scripts/models/todo-model.js"></script>
<script src="scripts/views/todos-view.js"></script>
<script src="scripts/views/todo-view.js"></script>
<!-- endbuild -->
```

How 'bout that! It not only created and placed files in relevant directories, it even included them in your HTML for you.

I've created a repository for what our To Do application will look like. [Click here](https://github.com/stephenplusplus/tutorial-backbone-app) to see the code. We'll walk through the files together to some degree, but please refer to the repository to get the full code.

### `scripts/main.js`
```js
/*global backboneApp, $*/
'use strict';

window.backboneApp = {
    Models: {},
    Collections: {},
    Views: {},
    Routers: {},
    init: function () {
        new this.Views.TodosView({
            collection: new this.Collections.TodosCollection()
        });
    }
};

$(document).ready(function () {
    backboneApp.init();
});
```
#### Thoughts
The Backbone generator is establishing some good practices you can use right out of the box. It took the name of your directory, in my case "backboneApp", and exposed an object literal to hold the Models, Collections, and other objects we'll create.

The generator also incorporates [JSHint](http://www.jshint.com) into your app's build process, making sure your code is of the highest quality. You are encouraged to customize your preferences inside the `.jshintrc` file in the root of your project's directory.

You'll also see `'use strict';` at the top, which kicks your app into [Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode).

Finally, the `$(document).ready` will call `backboneApp.init`, which creates a `TodosCollection`, then passes it into a `TodosView`. I'll go over these in more detail soon.


### `scripts/collections/todos-collection.js`
```js
/*global backboneApp, Backbone*/

backboneApp.Collections.TodosCollection = Backbone.Collection.extend({

    localStorage: new Backbone.LocalStorage('backbone-generator-todos'),

    initialize: function () {
        this.model = backboneApp.Models.TodoModel;
    }

});
```
#### Thoughts
If we want our To Do app to be somewhat usable, we have to store our To Do items somewhere. There's a handy Backbone adapter you may be familiar with, called Backbone.LocalStorage. It will intercept Backbone's calls to the default remote backend, and use your browser's `window.localStorage` instead.

We know we'll need the Backbone.LocalStorage adapter, but we don't know where we'll get it. Idea! Idea! Bower.

We haven't made much use of Bower directly. When our application was scaffolded, Bower was used behind the scenes to grab Modernizr, Twitter Bootstrap, jQuery, Underscore, and Backbone. But, what if we want to add in another JavaScript library?

Go back to your favorite terminal and try this:

```
$ bower search backbone
```

Ok, wow. That's... a lot. Maybe we should narrow that down.

```
$ bower search backbone.localstorage
Search results:

    backbone.localStorage git://github.com/jeromegn/Backbone.localStorage.git
```

There we go. Now we just have to install it.

```
$ bower install backbone.localStorage --save
bower cloning git://github.com/jeromegn/Backbone.localStorage.git
bower cached git://github.com/jeromegn/Backbone.localStorage.git
bower fetching backbone.localStorage
bower checking out backbone.localStorage#v1.1.4
bower installing backbone.localStorage#v1.1.4
```

When working with multiple developers, it can be troublesome assuring everyone has the correct dependencies and matching versions. By using `--save` above, we are telling Bower to remember this new dependency, then write about it in our `bower.json` file. When another developer clones your project, they just have to run `bower install` to download every dependency, thus keeping everyone in sync. That's why `app/bower_components` is listed in your `.gitignore` file. Gone are the days of bloated repositories!

Now that Bower has awesomed all over our application, go into `app/index.html` and update the `scripts/vendor.js` comment block:

```html
<!-- build:js scripts/vendor.js -->
<script src="bower_components/jquery/jquery.js"></script>
<script src="bower_components/underscore/underscore.js"></script>
<script src="bower_components/backbone/backbone.js"></script>
<script src="bower_components/backbone.localStorage/backbone.localStorage.js"></script>
<!-- endbuild -->
```

When you save the file, your browser will refresh and you'll have the new library ready to use. More importantly, our `TodosCollection` will have it ready to use.


### `scripts/collections/todo-model.js`
```js
/*global backboneApp, Backbone*/

backboneApp.Models.TodoModel = Backbone.Model.extend({

    defaults: {
        title: '',
        completed: false
    },

    toggle: function () {
        this.save({
            completed: !this.get('completed')
        });
    }

});
```
#### Thoughts
This is a pretty basic Backbone Model. We set some default properties for our To Do items, and define a `toggle` function, simply used to switch between a "Completed" or "Incomplete" state.


### `scripts/views/todos-view.js`
```js
/*global backboneApp, Backbone, JST*/

backboneApp.Views.TodosView = Backbone.View.extend({

    el: '#todo-app',

    template: JST['app/scripts/templates/todos.ejs'],

    events: { /* ... */ },

    initialize: function () { /* ... */ },

    render: function () { /* ... */ },

    createTodo: function () { /* ... */ },

    addTodoItem: function () { /* ... */ },

    addAllTodoItems: function () { /* ... */ }

});
```
#### Thoughts
This is our must robust Backbone View, so to see the definitions to these various properties and methods, please refer to the [repository](https://github.com/stephenplusplus/tutorial-backbone-app).

However, here are a couple key things:

```js
el: '#todo-app'
```

This selector matches that `<section id="todo-app"></section>` element we created in our `index.html` file. This will be our primary View.

```js
template: JST['app/scripts/templates/todos.ejs']
```

This little JST thing snuck in when we said `yo backbone:view ____`. When our View's JavaScript file was created, it also created a template file for us: `app/scripts/templates/todos.ejs`.

This lets us define our View's HTML in a separate file, which is collected into a JavaScript object, `JST`, then used as our template.


### `scripts/templates/todos.ejs`
```html
<form class="input-append">
    <input type="text" id="new-todo" placeholder="What do you need to do today?">
    <input type="submit" class="btn">Submit</button>
</form>
<ul>
    <!-- Where our To Do items will go -->
</ul>
```
#### Thoughts
Because we answered "Yes" to including Twitter Bootstrap for Sass when we scaffolded our application, I've added a couple of class names to pretty up our app. Feel free to style to your heart's content in the `styles/main.scss` file.


### `styles/main.scss`
```css
@import 'sass-bootstrap/lib/bootstrap';

.hero-unit {
    margin: 50px auto 0 auto;
    width: 300px;
}

form {
    margin-top: 10px;
}

ul,
li form {
    margin: 0;
    padding: 0;
}

ul {
    list-style: none;
}

li form {
    display: none;
}

.editing {
    span {
        display: none;
    }

    form {
        display: inline-block;
    }
}

input:checked ~ span {
    text-decoration: line-through;
}
```
#### Thoughts
Sass is pretty cool.

Also, it's pretty cool that the browser still reloads when you make a change to your Sass files. If you've used Sass before, you know it can be somewhat of a hassle to get a productive development environment set up. Out of the box, you're editing, watching, and reloading with none of the aforementioned hassle. Smiley face.


### `scripts/views/todo-view.js`
```js
/*global backboneApp, Backbone, JST*/

backboneApp.Views.TodoView = Backbone.View.extend({

    tagName: 'li',

    template: JST['app/scripts/templates/todo.ejs'],

    events: {
        'click input[type="checkbox"]': 'toggle',
        'dblclick span': 'toggleEdit',
        'submit form': 'toggleEdit'
    },

    initialize: function () { /* ... */ },

    render: function () { /* ... */ },

    toggle: function () { /* ... */ },

    toggleEdit: function () { /* ... */ }

});
```
#### Thoughts
This `TodoView` will represent an individual item. It will be an `<li>` with some custom functionality, handling click, double click, and submit events, enabling a user to edit and save a To Do.


### `scripts/templates/todo.ejs`
```html
<input type="checkbox" <% if (completed) { %>checked<% } %>>
<form>
    <input type="text" value="<%= title %>">
</form>
<span>
    <%= title %>
</span>
```
#### Thoughts
Simple enough. We're using some basic Underscore templating to spit out values and toggle a `checked` state on our checkbox.


## To Do: To Do It Again

Our To Do application is actually done! It's quite basic in functionality, but you can feel how natural it is to develop an application using Yeoman and his Generator buddies. And even though the functionality is basic, none of the techniques we used to get here were "basic." We're using smart, efficient libraries (Sass, Backbone, Underscore) with a finely-tuned development process (Grunt, LiveReload, Compass), and it took us only a few terminal commands.

If you're like me, you probably want to stop with the To Do stuff, and start making your own applications. You should now be familiar with the development workflow, so you're free to go explore. You'll learn even more when starting from scratch, having your own app in mind.

If you want to go play around, go ahead! When you're done generating like a crazy person, come back and let's ship it.


## To Do: Ship It

Let's put this thing in the water and see if she floats! DO NOT put your computer in the water. Wait, would a MacBook Air float? No, probably not. Right?

That was a dangerous paragraph. Let's just get our app ready for production, safe and dry.

`grunt server` has been amazing, but it's time to meet his brother, `grunt build`. We talked about him a bit earlier, but let's go over a few more details.

Here is what the `grunt build` task is defined as in your `Gruntfile.js`:

```js
grunt.registerTask('build', [
    'clean:dist',    // Clears out your .tmp/ and dist/ folders
    'coffee',        // Compiles your CoffeeScript files (if any)
    'createDefaultTemplate', // Creates a JS file that sets up your JST object
    'jst',           // Compiles your `scripts/templates/` files
    'compass:dist',  // Compiles your Sassiness
    'useminPrepare', // Looks for those <!-- special blocks --> in your HTML
    'imagemin',      // Optimizes your images!
    'htmlmin',       // Minifies your HTML files
    'concat',        // Task used to concatenate your JS and CSS
    'cssmin',        // Minifies your CSS files
    'uglify',        // Task used to minify your JS
    'copy',          // Copies files from .tmp/ and app/ into dist/
    'rev',           // Creates unique hashes and re-names your new JS/CSS files
    'usemin'         // Updates the references in your HTML with the new files
]);
```

So, that thing is pretty legit. All of these tasks are defined inside of `Gruntfile.js`, so feel free to poke and tweak around to tailor the experience to your needs. It's highly likely you won't need to do any customization at all, but it's there if you need to!

One other thing. `grunt build` is actually wrapped inside of another task.


### `grunt`

Simply running `grunt` will execute the `default` task:

```js
grunt.registerTask('default', [
    'jshint',
    'test',
    'build'
]);
```

Those first two tasks, `jshint` and `test` are easy to overlook when rushing an app out the door, but are very important.

### JSHint
The `jshint` task will check with your `.jshintrc` file to learn your preferences, then run it against all of your JS files. To get the full run down of your options with JSHint, check [the docs](http://www.jshint.com/docs/#options).

### Test
The `test` task looks like this:

```js
grunt.registerTask('test', [
    'clean:server',
    'coffee',
    'createDefaultTemplate',
    'jst',
    'compass',
    'connect:test',
    'mocha'
]);
```

It basically does enough to create and serve your application for your test framework, Mocha, to execute your tests.

Oh crap, tests.

Next door to your `app/` and `dist/` directories, this little `test/` buckaroo has been waiting for our attention. Aww.

IF you open that up, you'll see `test/` has its own `bower.json` and `index.html`, as well as a `spec/` directory. Your tests will have some dependencies of their own, the [Chai Assertion Library](http://chaijs.com) and [Mocha testing framework](http://visionmedia.github.io/mocha).

Expand that `spec/` directory and you'll see a `test.js` file that looks something like this:

```js
/*global describe, it */
'use strict';

(function () {
    describe('Give it some context', function () {
        describe('maybe a bit more context here', function () {
            it('should run here few assertions', function () {

            });
        });
    });
})();
```

Ok, looks like we could use [a pull request](https://github.com/yeoman/generator-backbone/pulls) to correct some grammar. Anybody?

If you haven't written your own tests before, you'll see terms like `describe`, `it`, `before`, `beforeEach`, `after`, and `afterEach` pop up. `describe` is a wrapper for a group of related tests, and each `it` is a specific test.

Try running a `grunt test` to see all the magic unfold.

```
$ grunt test
Running "clean:server" (clean) task
Cleaning ".tmp"...OK

Running "coffee:dist" (coffee) task

Running "coffee:test" (coffee) task

Running "createDefaultTemplate" task

Running "jst:compile" (jst) task
File ".tmp/scripts/templates.js" created.

Running "compass:dist" (compass) task
directory .tmp/styles/
   create .tmp/styles/main.css

Running "compass:server" (compass) task
unchanged app/styles/main.scss

Running "connect:test" (connect) task
Started connect web server on localhost:9000.

Running "mocha:all" (mocha) task
Testing: http://localhost:9000/index.html

  ․

  1 test complete (1 ms)

>> 1 passed! (0.00s)

Done, without errors.
```

You should play around and see if you can write some tests for our To Do application. A couple ideas for test cases:

- Does creating a new To Do item get stored in localStorage?
- Does a new To Do item's title get trimmed?
- When editing a To Do item, does changing it to "blank" then saving remove the To Do item from localStorage?


### Press Enter

```
$ grunt
```

You should see our favorite words: `Done, without errors.`


## Yo' Next Application

Yeoman is still brand new, with pull requests and new ideas coming in every day. I truly believe it's something every developer should at least try. If you give it a shot and find it's not suitable for your task, I and the rest of the team would love to hear why.

If you need a buddy to help you with your project and Paul Irish is busy doing... [this](http://www.youtube.com/watch?v=0DQwOSbFB5Y), come find me. I'm always in the [#yeoman freenode room](http://webchat.freenode.net/?channels=yeoman), or just ping me on Twitter. I'm [@stephenplusplus](http://twitter.com/stephenplusplus), or Stephen Sawchuk. Nice to meet you.
