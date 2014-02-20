# Train Your Mental Interpreter

One of my best buddies, [@passy](https://twitter.com/passy), wrote up an awesome post, [Partial Application in JavaScript using bind()](http://passy.svbtle.com/partial-application-in-javascript-using-bind), which demonstrates a way to use `.bind()` in a way you may not have thought was possible.

A quick excerpt:

> You probably all know of Function.prototype.bind. … The first argument passed to `bind` will serve as `this` within the scope of the function it returns. A lesser known property of `bind` is that it accepts more than one parameter. *Every parameter to `bind` after the first will be prepended to the list of parameters when invoking the bound function.*

> - Pascal Hartig - [Partial Application in JavaScript using bind()](http://passy.svbtle.com/partial-application-in-javascript-using-bind)

Introducing yourself to a new type of trick like this is more than just picking up a tip on how to re-factor your code; it requires re-thinking how your mental JavaScript interpreter works. You will carry it with you every time you `touch` a new file. That's exactly the type of thing we love about JavaScript&mdash; you can go years doing things one way, then read a post, or check out someone else's code on GitHub, and learn to see things entirely differently.

### A Real-Life Use Case

Last week, I needed to create a function that had one basic responsibility: update the title of the document based on the active route in an Angular app.

In each of the code snippets below, the results of these expressions will always be the same:

```js
updateTitle();        // The Best Blog Ever
updateTitle('Intro'); // Intro | The Best Blog Ever
```

#### So, here's what my function ended up looking like...

```js
function updateTitle(title) {
  var defaultTitle = 'The Best Blog Ever';

  if (title) {
    document.title = title.trim() + ' | ' + defaultTitle;
  } else {
    document.title = defaultTitle;
  }
}
```

I got to thinking, for such a simple thing, couldn't this be a little shorter?

#### Sure, I could have done this...

```js
function updateTitle(title) {
  var defaultTitle = 'The Best Blog Ever';

  document.title = title ? title.trim() + ' | ' + defaultTitle : defaultTitle;
}
```

#### ...or something trickier...

```js
function updateTitle(title) {
  var defaultTitle = 'The Best Blog Ever';

  document.title = (title && title.trim() + ' | ' || '') + defaultTitle;
}
```

#### But, y'know. What if I tried that fancy `bind()` "partical application" thing?

```js
var updateTitle = function (defaultTitle, title) {
  document.title = (title && title.trim() + ' | ' || '') + defaultTitle;
}.bind({}, 'The Best Blog Ever');
```

## That's it? Great, this was a waste of time.

Yeesh. Sorry.

Maybe you realized you could use `.bind` this way a long time ago. Maybe it's always been obvious to you, and you *choose* not to use it.

Please note you should always prefer and encourage readability in your code. You will never catch me spending time optimizing characters for no reason. This wasn't that. This was a quest to **train my mental interpreter**. That's what it takes to learn new things; being honest with yourself about what you didn't know you could do. This post is me sharing my honesty with you.
