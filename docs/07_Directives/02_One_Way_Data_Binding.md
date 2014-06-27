These are the built-in directives that bind data to an HTML element or elements.  All of them can be applied using an attribute call, or (a little less comfortably) a class definition.

	<p ng-bind="scopeProperty"></p>

	<p class="ng-bind: scopeProperty"></p>

Data binding is the central aspect of Angular's awesomeness.  Most applications will have very sparce snippets of HTML not bound to any data.  When we speak of data-binding, what means is that when the data model changes, the view is updated to reflect the new data model.  This is all done by the functions defined in the controller - hence the concept of model-view-controller.

##Performing One-Way Bindings##

The most basic calls for one-way bindings are done with `ng-bind` (as demonstrated above), or the `{{...}}` syntax applied within the content of an HTML element.

`ng-bind` will apply the data bound to the HTML element within the content of the element, using the `innerHTML` property.  So, on the example above, there will be nothing else in the `<p>` element, even if the template is written with text between the opening and closing tag.  Angular will replace it with the data bound by `ng-bind`, with `innerHTML` overwriting whatever content was originally there.

Conversely, using the `{{...}}` syntax will apply the data inline with any other HTML, whether or not it's the only HTML in the element.

	<p>Hello {{data.world}}!</p>

To add to `ng-bind` inline, you can do this by applying it to a `<span>` element (or break syntax and apply it to any other inline element, really).

There is a templated expansion to the `ng-bind` directive that can prove more useful - the `ng-bind-template` directive.  By using this as an element's attribute, you can set the template to the data-binding by combining the function of `ng-bind` with inline `{{...}}` notation:

	<p ng-bind-template="First you should {{scopeArray[0].action}}; then you should {{scopeArray[1].action}}.  Let me know if you have any questions."></p>

It looks a bit cumbersome, and admittedly it is.  There are better ways to do things, so this one probably won't be used very much.

##Preventing Inline Binding##

One of the drawbacks of inline binding is that it automatically looks for `{{...}}` and binds whatever data it can, sometimes removing it altogether if it can't find data to bind.  This can be a huge drawback if you're using other JavaScript libraries that use a similar notation (Handlebars, Meteor, etc.), or if you (for some reason) use double-braces in your own text.

The data-bind cancellation directive that's built into Angular is `ng-non-bindable`.  Apply this to any HTML element, and whatever `{{...}}` you put inside will remain unattended by Angular, leaving you free to do whatever.