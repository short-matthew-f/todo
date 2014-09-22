# Part I: Getting todos from the form to the list.

### Part I-A: Stopping those pesky submits
So you have a form, presumably it looks something like this:

```html
<form>
  <input type="text" placeholder="Type your todo here.">
  <button type="submit">Click me to add it!</submit>
</form>
```

Remember, the usual way we write form tags is as follows:

```html
<form action="some_url" method="post">
  ...
</form>
```
Normally when you smack that submit button, the browser fires off a request to `some_url` with the method, in this case, `POST`.  (By the way, if your tag is missing the method attribute, it will default to a `GET` request.)  This will cause a page refresh as the server returns the result of this request, which is something we wish to avoid.

Let's start by adding a handler to the form that prevents the normal submission action.  We need to grab the form and wrap it into a jQuery object.  While you're at it, put it in a variable for future use, like so:

```html
<script>
  var $todoForm = $('form')
</script>
```


Now that we've put it somewhere, we can add some functionality to it.  jQuery has an excellent handler called `submit`, which fires off a function of your choosing when the corresponding form is submitted.  Step one is usually to prevent the default action, like so:

```html
<script>
  var $todoForm = $('form')
  $todoForm.submit(function(event) {
    event.preventDefault();
  });
</script>
```

Go ahead and reload your page, and try clicking the submit button.  If nothing happens, then good for you!

### Part I-B: Doing something other than doing nothing

#### Grabbing the input

Ok, so not submitting is great, but we need to figure out how to grab the text from the input box, and moving it into the list.  Let's start with getting the text from a submitted form.

There are a few ways to do this, one is to serialize the entire form into an array via `.serializeArray()` ([Reference here](http://api.jquery.com/serializeArray/))  This is great when your form has many fields, and you need to grab them all to do something.

Here, we have but one field, so I chose to take the easy way out.  Update your script to the code below, and see what happens.  Make sure you've got the developer console up before clicking submit.

```html
<script>
  var $todoForm = $('form')
  $todoForm.submit(function(event) {
    event.preventDefault();

    console.log($('input').val());
</script>
```

If all went well, you'll notice that whatever you typed in your input box appears in the developer console.  So if you grab a particular input field, you can extract what's in it at the time of submit with the `val` method.

##### Using jQuery to create new html elements

How do we create and drop in a new list element?  You might remember that the jQuery wrapper, `$`, has many capabilities.

First, we can grab existing dom elements and wrap them into jQuery objects.  Remember that we will often append a `$` to the front of any variable representing a query object.  It's incredibly useful to have a reminder.

```javascript
var $allParagraphs = $('p');
var $itemsWithClassCompleted = $('.completed');
var $thingsWhichHaveIDImportant = $('#important');
```

But also we can create a totally new element as so:

```javascript
var $neverBeforeSeenSpan = $('<span>');
```

See, by wrapping a tag with the jQuery object, you get back a jQuery object that has that tag inside of it.  It's super useful, and incredibly flexible.  Try the following in your console:

```javascript
> var $li = $('<li>');
> $li.css("background", "yellow");
> $li.text("HELLO THERE!");
> $('ul').append($li);
```

A poorly styled, yellow box with HELLO THERE! in it should have appeared at the end of your list.  In addition to methods `css` and `text`, there's also things like `addClass`, `html`, `attr` (useful for adding things like `id` or `role`).

Suppose you have `<div id="future-home-of-ul"></div>` in your html.  Examine the following code, and guess what it will do.

```javascript
var thingsToList = [
  "go to store",
  "eat a banana",
  "rotate tires",
  "rotate self"
]

var $futureHomeOfUl = $('div#future-home-of-ul');
var $ul = $('<ul>');

for (var i=0; i<thingsToList.length; i++) {
  var $li = $('<li>').text(thingsToList[i]);
  $ul.append($li);
}

$futureHomeOfUl.append($ul);
```

What it does:
* Creates an array storing the things we wanted to do
* Grabs the div that will be used to display the list
* Creates a `ul`
* Iterates over the array, making a new `li` for each element of the array, and adding it to the end of the `ul`.

It's really quite nice.  We totally created a useful piece chunk of `html`, and were able to place it in the dom. At the end you get the following:

```html
<div id="future-home-of-ul">
  <ul>
    <li>go to store</li>
    <li>eat a banana</li>
    <li>rotate tires</li>
    <li>rotate self</li>
  </ul>
</div>
```

### Putting it together, AKA: Your turn!

Now that you've been given enough information, add the following things to your submit handler:

1. Take the user input from the form, store it in a variable
2. Create a new list element, set the text to the user input
3. Add the list element to the unordered list

You may notice that it might not look like your previous list.  There won't be any styling unless you use jQuery to add it as you go.  Remember that you can add classes and other attributes to each element.  Go back and fix it if you didn't the first time around.  Now you should be able to add new things and have it look right.

### Part I-C: Our first bug

So, in addition to typing things in your form and having them appear in your list, just hit enter in a blank box.  What happens?  You're adding blank todos to your list.  That's not terrific.

We can use a little JavaScript to fix this.  You'll have to edit your submit handler for the form, and add a piece of code to first check to see if the input text is blank or not.  It's pretty simple to do.  We'll use an `if` statement to check the input, and only add it to the list if it's not blank.  Remember the syntax for these conditionals?

```javascript
// if syntax
if (condition) {
  doSomething;
};

// if-else syntax
if (condition) {
  doSomething;
} else {
  doSomethingElse;
};
```

We want to say IF input isn't blank THEN add it to the list.  Try moving your code around to make it work.  Once you can only add things with at least one character (even a space), call over the instructor for a quick code review.

# Next step

Go to [Part II](https://github.com/short-matthew-f/todo/blob/master/part_ii.md).