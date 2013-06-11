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
This is actually a separate plug-in, or "generator," called `generator-webapp`. Yeoman recognizes other `generator-____` Node modules, which opens the door for Backbone, AngularJS, and countless other you-name-it generators.

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
Nobody likes going to GitHub or random developers' sites to download a .zip of a JavaScript tool. Like when fetching a Node package with `npm install ___`, Bower lets you say `bower install ___`. The component is then saved in a directory of your choosing, generally, `app/bower_components/` for Yeoman-generated apps. Assuming you wanted jQuery, you would `bower install query`, then include the relevant file inside of your HTML file, `<script src="bower_components/jquery/jquery.js"></script>`


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

At this point, `yo` has done his job. He's given you everything you need to launch a production-ready web application. Let's now shift our focus to what Grunt tasks he's pre-configured us with.

### `grunt build`

Running `grunt build` takes your `app/` source code files and turns them into a distributable application, which ends up in `dist/`.

That `dist/` folder is what you feed to your server. `dist/` will have it's own `index.html`, with references to minified and concatenated `dist/scripts` and `dist/styles`, and optimized `dist/images`. Your users will appreciate this. Your phone-card, dial-up users will __really__ appreciate this.

Behind the scenes, `grunt build` is a task that runs several sub-tasks. One of those is [`grunt-contrib-usemin`](https://github.com/tinganho/grunt-contrib-usemin), which looks for blocks inside of your `app/index.html`, like this:

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

`open:` Opens the server instance, typically `localhost:3000` in your browser

Make an edit or two in the source files to see the change reflected in the browser. Like I said above, this is about as easy as it can be. It just works.


## Let's App It Up!

I of course meant appetizers. Grab some cheese sticks, then meet me in a little bit.

*Wash your hands!*


## Let's Create an Application

Let's not get too crazy with this application. You probably have your own ideas for what you're looking to create. Like Yeoman himself, I won't tell you what to do, I'll just help you do it-- with one caveat: let's use Backbone to see how other generators work!

Real quick:

```
# install the Backbone generator:
$ npm install -g generator-backbone

# make another play directory, then run:
$ yo backbone
```

Again, pop in a couple `No`s so we're on the same page.

Things should feel quite familiar after our experience with the web app generator. You still have an `app` directory, with `scripts/`, `styles/` and an `index.html`.

Before we start editing files, run:

```
$ grunt server
```

As we talked about earlier, this starts the server, sets up watches on our files, blah blah yipsie-doodle.

