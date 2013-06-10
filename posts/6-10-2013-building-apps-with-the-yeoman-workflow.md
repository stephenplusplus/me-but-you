# Building Apps With The Yeoman Workflow

## What is Yeoman?

Trick question. It's not a thing. It's this guy:

** image **

Basically, he wears a top hat, lives in your computer, and waits for you to tell him what kind of application you wish to create. He comes bundled with a simple "web app" generator, that will do something like this:

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
[?] Would you like to include Twitter Bootstrap for Sass? (Y/n)
```

Whoa, nelly!

One, OMG so dreamy.

Two, thanks, bro.

All we did was tell him what we wanted, and he replied with a specific question to give us even more customization.

Let's go back a step, though. Not every new computer comes with a Yeoman pre-installed. He lives in the NPM package repository. You only have to ask for him once, then he packs up and moves into your hard drive. _Make sure you clean up, he likes new and shiny things._

`npm install -g yo`

You now have a brand new Yeoman. He's a person with feelings and opinions, but he's very easy to work with. If you think he's too opinionated, he can be easily convinced.

Let's take a second to break apart what that `yo webapp` command really did.

### `yo`
OS X, Linux, and Windows friendly system-wide command, that scours your hard drive for any installed "generators," then gives them control based on the next argument:

### `webapp`
This is actually a separate plug-in, or "generator," called `generator-webapp`. Yeoman recognizes other `generator-____` Node modules, which opens the door for Backbone, AngularJS, and countless other you-name-it generators.

Something important to take away from that is, it's the `generator-webapp` module that prompted us with those questions. That also goes for any other generators we install. They are maintained by the community, not necessarily the Yeoman team members themselves.

By using Yeoman, you're not saying "I want to do things your way, master. *bow* *bow*," without having any control. You're just saying, "I want to make an application that follows best practices, discovered by frequent users and contributors of the web development community."

Seriously, you have to say it just like that, or it won't work.

Should you prefer to do something differently than what he gives you, you simply change the code that was generated for you, or even go to the source of the "generator" itself, and send in your contribution.


## Friendship

Our buddy, yo has some buddies of his own, and thinks you'll all get along over endless tea and smiles. If you haven't heard of [Grunt](http://gruntjs.com) or [Bower](http://bower.io), here's a quick summary of what these give us:

### Grunt
A JavaScript-based task runner, that does the dirty stuff. Like `yo`, it also provides a base set of functionality, then allows the community to share their own plug-ins, or "tasks" that help accomplish common things. When you scaffold your application with `yo webapp`, Grunt and some hand-picked tasks will come along, which accomplish things like running your website in a local development environment, concatenating and minifying your code, optimizing your images, and much more. Tasks are run through the command line, by typing `grunt server`, `grunt build`, `grunt test`, and many more.

Tasks are defined and customized in a `Gruntfile.js` file, which lives in the root directory of your project. Check it out to see what Yeoman set up for you.

### Bower
Nobody likes going to GitHub or random developers' sites to download a .zip of a JavaScript tool. Like when fetching a Node package with `npm install ___`, Bower lets you say `bower install ___`. The component is then saved in a directory of your choosing, generally, `app/bower_components/` for Yeoman-generated apps.

