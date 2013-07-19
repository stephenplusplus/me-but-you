# Bower Conventions

## What is Bower?

[Bower](http://bower.io) is a package manager for client-side code. This can be Sass stuff, CSS stuff, but mostly JavaScript stuff.


## A [fake] conversation with a package author

### How do I use Bower?

Like, to register your plug-in or whatever?

### Yeah!

Oh, you just make a `bower.json` that looks like:

```
{
  "name": "name-of-your-thing-with-hyphens",
  "version": "0.0.0-semanticVersion",
  "main": "theFileYouAreDistributing.js",
  "dependencies": {
    "dependencyOne": "0.0.0-itsVersion"
  }
}
```

### Semantic version?

[Yeah, semver](http://semver.org). It's pretty basic. If everyone follows the same system, it lets our different plug-ins and projects work together seamlessly.

### Oh, cool. Like how NPM does--

Yeah! Exactly, just how NPM does it.

### Makes sense. So, the "main" file.

Yep.

### Well, first, does it matter how I structure my repo?

No! What will happen is, that version you specified in your `bower.json`--

### --the semver thing?

Yeah. That will match a tag in your repo.

### A git tag?

Yes, sir.

### So I'll make a tag called "0.1.0" or whatever, and that will be what is installed when someone runs `bower install unicornPopsiclePlugin`

Yes!

### …

…

### Nothing, I just thought you would ask me about the unicorn popsicle plugin.

…

### Nevermind.

Done.

### So, back to the structure of my repository. Does it matter?

No! You can throw it all in there.

### Ok, but, is that a good idea?

No.

### So, why does it let me?

Iunno. 'Cause it's the internet, and you can do whatever you want.

### Okay, you're getting crabby.

Sorry. So, you can include your whole repository, but that would indeed be bad, as you pointed out. When a developer says `bower install unicornPopsiclePlugin`, they don't want your crazy build files, images, and other junk. They just want the actual file they'll be including in their app.

### Right, the one I set as `main` in `bower.json`.

Yep. Speaking of `bower.json`, there's another property most developers either don't know about, or don't care about.

### Watch the crabby.

Sorry.

It's called `ignore`, and is an array that lets you specify what files and folders shouldn't ship out to the user when they install your unicorn.

### A unicorn can't be installed. You're being ridiculous.

So, anyway. Once you have all of those things in place, you just `bower register` your plugin, and your unicorn will finally be free.

### Oh, thank God.


## A [fake] conversation with a developer

### How do I use Bower?

$ npm install -g bower

$ bower install jquery

### No, I mean, how do I USE Bower?

I just answered that.

### No, like, what do I-- nevermind.

:( No, really, what?

### Like, let's say I just installed my favorite plug-in in the world, `unicornPopsiclePlugin`. It goes in some `bower_components/unicorn-popsicle-plugin` directory.

Ok. What's wrong with that?

### Well, nothing. But, what do I do with it? I have an `assets/vendor/` directory where I already have my jQuery, Modernizr, and other stuff. How do I get it to install there?

Oh, that's easy. Just create a `.bowerrc` file in the root directory of your project that says:

```
{
  "directory": "assets/vendor"
}
```

### Oh, snap. Awesome, lemme try it out.

Doot doo doo.

### Ok, I ran `bower install unicornPopsiclePlugin` and it… hey! It worked!

Sweet!

### Wait.

Doot doo doo.

### So, it installed it there, but, um, there's like, a million images of unicorns.

Oh, my God. I told him not to do that.

### My `assets/vendor` directory doesn't have subfolders. It's just the .js files I need. I have a build script that squashes these files into one and minifies them.

Ah.

### So… do I have to copy only the file I need into a… new file…?

Well. In this case, yes.

### How did Bower make anything easier?

This is where Bower gets a lot of blame. Let's walk through this, and target the real problem.

First, the package author chose to ignore my advice of only including the important files to his plug-in. He could easily have stripped out the images and whatever other junk is in there.

### Oh, really?

Yeah, it's the easiest thing in the world. Not sure why he didn't.

### But even if he did, I need all of my dependency files in the same folder.

About that. Can you just change your build script to not be so picky? Have it look inside a directory for a file.

### I guess I could do that.

Does that system even work, anyway? How do you prioritize the files, so that the files are concatenated in the correct order?

### Every file is in a big array in my build script. They get squashed in the order I list them.

… Well, ok. Do that, then. Just say the file is in `vendor/jquery/jquery.js` or whatever.

### Alright. But, I thought Bower was going to make this stuff seamless.

Bower is a bird, not a unicorn.

### Fair enough.


## Key points:

If you're a package author, please consider the developer I just [pretend] spoke to.

- Use the `ignore` array. We don't want extra junk. That's extra HD space, download times, and confusion. We only want the files that are absolutely necessary to get your thing working.

- Use the `main` property. There are tools out there that are trying to make the developer's life easier by wiring up their Bower components into their require.js configuration, or index.html file, etc. These tools can't sift through 35 JavaScript files and reliably detect what the actual file to include is.

- Don't talk to pretend people. I'm losing my mind.
