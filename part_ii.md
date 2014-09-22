# Part II - Adding some panache

Now that we've added the todos to the list, we want to bring the list to life with the ability to rearrange, confirm, and cancel the todos.

### Sorting

This one is totally going to be on you.  Head over to [Sortable](http://jqueryui.com/sortable/), and implement it on your todo list.  Reload, create a few todos, and then rearrange them.  Congrats!

### Remember those buttons?

Currently, you have the "buttons" (in quotes, because they are probably actually just `divs`) to the right of your text that don't do anything.  Let's change that.

Presumably your buttons have classes like `confirm-todo` and `cancel-todo`, or something like that.  We can add click handlers to those elements, and have them do something useful.

First, let's work on confirm.  When we confirm a todo, we want to remove the ability to cancel it, and permanently mark it as finished by changing the class of the checkmark button to green.  It'll look something like this:

```javascript
$('#todo-list').on("click", ".confirm-todo", function(event) {
  // add .finished class to .confirm-todo div
  // remove nearest .cancel-todo
});
```

When we're inside the function above, the `div` we clicked (with the `.confirm-todo` class) is called `this`.  So if we want to perform jQuery functions, like `addClass` to that `div`, we just wrap it in a jQuery object.  `$(this).addClass('class-name');` or `$(this).siblings().hide();`, etc.

**Hint, hint**: see previous paragraph to finish adding the confirm functionality.

Also, we should make the cancel button do something, too.  I thought it would be nice to slide it up before deleting it forever from the dom.  Here's my code:

```javascript
$('#todo-list').on("click", ".cancel-todo", function(event) {
  $(this).closest('li').slideUp({
    complete: function () {
      $(this).remove();
    }
  });
});
```

Let's talk about it.
* `$('#todo-list').on("click", ".cancel-todo"` adds a click handler to any element with `class="cancel-todo"` that is a descendant of another element with `id="todo-list"`.
* `$(this).closest('li')` grabs the nearest ancestor of `this` (our `.cancel-todo`), which is an `li`
* `slideUp()` slowly reduces the height of the `li` until it's hidden.
* We're passing an options hash (or options object) `{ complete: function() {} }` to our `slideUp` function, so that once the slide is complete we actually remove the `li` permanently from the dom.

**Bonus Question**: Why can't we do the following?

```javascript
$('.cancel-todo').click(function(event){
  $(this).closest('li').slideUp({
    complete: function () {
      $(this).remove();
    }
  });
});
```

Remember, `on("click",` and `click(` provide the same general functionality.  There's something deeper here thats going wrong.

# What did we do?

* We can drag and reorder list items
* We can cancel a list item
* We can confirm a list item

As usual, once you've implemented these features, call over the instructor to discuss your code.
