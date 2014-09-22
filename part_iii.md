# Part III - The Bonus Round

Now we want to be able to edit a todo.

* Only edit a todo which hasn't been confirmed
* Start editing if user double clicks the todo
* Stop editing if user submits edit or clicks anywhere else
* Don't allow sorting while editing

Since you're becoming an expert, we'll outline the details of what you'll have to do.

* Use `$().on("dblclick", ...` to detect double clicks
* Use `if(someTest) { return false; }` to prevent editing if the todo has already been confirmed.  `someTest` should check to see if the todo `li` has a `confirmed` class attached to it.
* You might need to go back and add one to your confirm function if you didn't before.
* `$( "#todo-list" ).sortable("disable");` exists
* You should create a form with one input, whose value is the current text from the todo.  You should then add it after the `li` you double clicked, and hide the `li` you double clicked.
* It will look like the list element transformed into a form, but you know better.
* `$('.todo-edit').focus().select()` will make things flow better for the user.
* You'll need to bind on "submit" or "focusout" to grab both ways a user might try to stop editing.
* `$( "#todo-list" ).sortable("enable");` exists

Struggle through this, you can do it!

Again, once you're done, go ahead and call over your instructor.

You should be proud of yourself.  You have a nice front end for a todo application.  Later on you can spin up a rails project to make the todos persist.
