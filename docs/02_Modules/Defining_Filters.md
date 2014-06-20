Filters are used to format the data displayed to the user.  In the simplest form, they can do some reordering and conditional presentation.  In more complex iterations, they can truly manipulate the data being displayed.

Once defined, a filter can be used across the module, meaning it can be used the same way throughout any controllers and views found within an Angular app.

A custom filter is technically a method of the Module object, and so it takes two parameters - the name of the filter, and the factory function that will be created when the filter is invoked.  Since filters are functions, they also receive data, and return that data reformatted according to whatever logic the filter passes that data through.  For example, let's say you want to filter the answer to a mathematical expression:

	<p>{{myPayCheck + yourPayCheck | mathFilter}}</p>

You would define `mathFilter` as:

	myApp.filter("mathFilter", function() {
		var error = "You've made a terrible mistake.";

		return function(input) {
			return angular.isNumber(input) ? input : error;
		}
	}

##Applying Filters##

In the HTML statement above, the filter is applied to the Angular expression, and then evaluates the result of that expression. The same would be the case if the expression was just a data property of the scope:

	<p>{{payCheckSum | mathFilter}}</p>

Filters are applied by adding a bar character `|` to the end of an Angular expression, and then naming the filter to be applied.  Filters are applied after the leading expression is evaluated, so logical and mathematical operators are welcome in the expression on which a filter is applied.

##Using Filters Globally##

Let's say you want to use a filter within a directive. You can do that! By passing the `$filter` service that Angular provides into the factory function argument of your directive, you can use that as a function within the directive, using the name of the filter as an argument. The `$filter` service gives access to any filter that has been defined on the Angular module.

Going off of the filter defined above:

	myApp.directive("thatDirective", function($filter) {
		var mathFilter = $filter("mathFilter");

		return function(scope, attrs, element) {
            if (mathFilter(scope.prop) == attrs['myDirective']) {
                element.css("color", "red");
            }
        }
    }

This will apply the `mathFilter` to the `scope.prop` value before comparing it to `attrs["myDirective"]`.  Keep in mind, a filter is a function, so it has to be treated like a function once it's passed to a local variable.  Thus, we're passing some scope data for it to filter.  In this case, it analyzes `scope.prop`, and either returns the value of `scope.prop` for comparison, or returns `"You've made a terrible mistake."`.