Directives are the most flexible aspect of AnguarJS, and therefore arguably the most fun.  There are plenty of directives that come built-in, but in many apps there will be a need to create new ones.  This is done with the `Module.directive` method.

	myApp.directive("myDirective", function() {
		return function(this, that) {
			// ... do stuff ...
		}
	});

The first function that's defined - the one passed as an argument to the statement creating the directive - is called a *factory function*.  It's called this because it creates the object that will be used by Angular to run whatever functions are found within.  The second function, which is returned, is called a *worker function*.  This is where the actual programming is executed when the directive is applied.

##Applying Directives to HTML Elements##

Applying directives to elements is done by passing them as an attribute, the same way you would with `class` or `id`:

	<div class="this-class" myDirective="someValue">

###Arguments that can be easily passed to Directives###

One of the benefits when working with directives is that it can easily be passed various data pertaining to the element and view on which it is being called.  For example, by passing `scope` (mind you, not `$scope`) to the worker function, you can access all of the data properties that are defined within the view's scope, as defined by the controller.

	myApp.directive("myDirective", function() {
		return function(scope) {
			if (scope.prop == "something") {
				doSomethingAwesome();
			}
		}
	}

The `attrs` argument provides access to all of the attributes that are applied to the element upon which the directive is applied.  That list also includes the directive itself, as an attribute.  So in some cases, you can pass data to the directive via the directive attribute.

	//...
		return function(scope, attrs) {
			if (scope.prop == attrs['myDirective']) {
				attrs['class'] = "awesome-class";
			}
		}
	//...

The `element` argument is actually an object created by jqLite, the Angular version of jQuery, which has been parsed down to include only Angular-specific bits.  This gives access to jQuery-like processes, such as the `css` method of the `element` object.

	//...
		return function(scope, attrs, element) {
			if (scope.prop == attrs['myDirective']) {
				element.css("color", "red");
			}
		}
	//...
