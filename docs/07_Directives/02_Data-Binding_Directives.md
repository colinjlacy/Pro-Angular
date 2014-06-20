These are the built-in directives that bind data to an HTML element or elements.  All of them can be applied using an attribute call, or (a little less comfortably) a class definition.

	<p ng-bind="scopeProperty"></p>

	<p class="ng-bind: scopeProperty"></p>

Data binding is the central aspect of Angular's awesomeness.  Most applications will have very sparce snippets of HTML not bound to any data.  When we speak of data-binding, what means is that when the data model changes, the view is updated to reflect the new data model.  This is all done by the functions defined in the controller - hence the concept of model-view-controller.

##Performing One-Way Bindings##

The most basic calls for one-way bindings are done with `ng-bind` (as demonstrated above), or the `{{...}}` syntax applied within the content of an HTML element.

`ng-bind` will apply the data bound to the HTML element within the content of the element.  So, on the example above, there will be nothing else