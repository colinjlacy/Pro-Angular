Calling the `ng-include` directive works like an include call in any other programming language, but in this case pulls in an `.html` file, in theory as a piece of a larger view.

Let's say I have an ordered list that I want to break out into an include.  It might start out looking like this:

	...
	<div id="list-parent">
		<h3>Some sweet list</h3>
		<ol>
			<li ng-repeat="item in items">{{item}}</li>
		</ol>
	</div>
	...

This is a very simple example and might not warrant breaking out, but it at least illustrates the point. In order to break that out, I'll save that bit in an `.html` file called `list.html`.  Once that's done, I can access it via the `ng-include` directive.

	...
	<div id="list-parent">
		<ng-include src="'list.html'"></ng-include>
	</div>
	...

Notice that in this case, the directive is used as an element, while the included file is passed to the `src` attribute.  The use for this attribute is pretty self-explanatory for anyone familiar with HTML.

The file path is also passed as a string literal within the attribute argument.  That's because whatever information is passed to the directive's `src` attribute is interpreted as a JavaScript expression, which is discussed below.

`ng-include` takes two other parameters passed as attributes on the element:

* `onload` - specifies an expression to be evaluated once the content of the included template is loaded - an animation, for example, or a change in style to a navigation item.
* `autoscroll` - specifies whether or not Angular should scroll the viewport when the content of the included template is loaded.

It's worth noting that Angular finds the template to be included, processes its directives first, and then includes the result in the parent template last.  Because it processes based on the parent template, it is processed with access to data model and behaviors defined by the controller attached to the parent template.

One way to think about these it so consider them often-repeated blocks of HTML or Angular expressions.  For example, if your templates are constantly calling on a short bio or avatar image, that could be broken out into an include.

###Calling includes dynamically, using expressions###

Since the `ng-include` directive's `src` attribute evaluates an expression by default, it's fairly straightforward to pass an Angular expression to the `src` argument, and use that to determine which file to include.

	// First set an input option for the user to interact with
	<div class="radios">
		<input type="radio" ng-model="include" value="list.html">List View
		<br/>
		<input type="radio" ng-model="include" value="table.html">Table View
	</div>

	// Then set the include depending on the user's selection
	<div id="list-parent">
		<ng-include src="include"></ng-include>
	</div>

In this example, we're defining the `src` argument by passing the `$scope.include` property, which we define using radio buttons and the `ng-model` directive.  Whichever value is chosen will be passed to the `$scope` and then used to determine the file path included.  Neat!

###Applying `ng-include` as an element attribute###

This directive works as an element attribute, with all the same rules applying.  The element the directive is applied to becomes the wrapper for the included template.  The `src` parameter becomes the default argument on the directive:

	<div ng-include="angular.expression"></div>

The other parameters of the `ng-include` directive become attributes of the element the directive is applied to:

	<div ng-include="angular.expression" onload="function()" autoscroll="truthyValue"></div>

This can be applied to any valid HTML element.

##Using `ng-switch` to fill content##

An alternate directive is `ng-switch`, which acts like a switch statement in JavaScript (and ultimately probably is).

	// First set an input option for the user to interact with
	<div class="radios">
		<input type="radio" ng-model="conditional" value="list">List View
		<br/>
		<input type="radio" ng-model="conditional" value="table">Table View
	</div>

	// Then set the include depending on the user's selection
	<div id="list-parent">
		<div ng-switch on="conditional">
			<div ng-switch-when="list">
				<!-- the HTML and directives associated with the list template -->
			</div>
			<div ng-switch-when="table">
				<!-- the HTML and directives associated with the table template -->
			</div>
			<div ng-switch-default>
				<!-- some default template content for when neither is chosen -->
			</div>
		</div>
	</div>

Notice that `ng-switch` is passed, in this case, as an attribute without an argument, and its parameter `on` is passed as an attribute as well.  If this were passed as an element, the `on` parameter would be an argument for the element.

It's always good to set a default fallback for the switch statement, say, for example, if nothing is chosen to set the switch in motion.  This is passed with another argument-less attribute, `ng-switch-default`.

A good way to think about using `ng-switch` as opposed to `ng-include` is to consider the main factor that separates them.  With `ng-switch`, the included HTML is loaded when the page loads, regardless of whether or not the user will access it.  So it's best to do this when it's well understood that the user will, in fact, use it - like the checkout process of a shopping cart. Also, since it's already loaded, it will cut down on the load time that's experienced when switching between templates using the `ng-include` directive.  Finally, since `ng-switch` is pre-loaded, it's generally suited to a specific use case, and unlikely to be repeated several times throughout the app - something `ng-include` is well suited for.