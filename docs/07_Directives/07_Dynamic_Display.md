One of the benefits of Angular is its ability to hide, show, remove, and add elements to the DOM conditionally and dynamically, based on expressions given to built-in directives.

##Showing/Hiding Elements##

This is one of the easiest ways to apply directives to elements, and gives flexibility by displaying something whether an evaluated statement is true or not.  Consider the following:

	// Previously defined, somewhere in the app...

	$scope.todos = [
		{ action: "Do this", complete: false },
		{ action: "Not that", complete: true }
	];

	// Now we apply it to the markup in an ng-repeat loop...

	<ol>
		<li ng-repeat="item in todos">
			{{item.action}} | <span ng-hide="item.complete">(Incomplete)</span>
							  <span ng-show="item.complete">(Done!)</span>
		</li>
	</ol>

In this above example, we'll have either "(Incomplete)" or "(Done)" displayed after the text of the `item.action`.  That's because the two `<span>` elements are hidden or shown, respectively, based on whether or not `item.complete` evaluates to true.  This works by either applying or removing a class called `ng-hide` (which is probably not the best design choice), which sets `{display: none}` on the element in question.  `ng-show` will do this if the statement evaluates false, while `ng-hide` will apply the class if the statement is true.

##Removing/Adding Elements##

Since the two directives above only show or hide based on CSS, the elements will still be accessible to the browser.  If we want to remove the elements altogether, we would do so using the `ng-if` statement, which will remove an element from the DOM if it proves false.

	// Using the same example from above, but rewritten to use ng-if on the two span elements

	<ol>
		<li ng-repeat="item in todos">
			{{item.action}} | <span ng-if="!item.complete">(Incomplete)</span>
							  <span ng-if="item.complete">(Done!)</span>
		</li>
	</ol>

These are data-bound statements, so if the data model changes - say, with a toggle checkbox for instance - the elements removed would be re-added to the DOM.

###Alternative to `ng-if`###

There are cases where `ng-if` won't work with other built-in directives.  For example, the following won't work:

    <li ng-repeat="item in todos" ng-if="!item.complete">
        ...
    </li>

In this case, it's better to apply a filter to the `ng-repeat` directive:

	<li ng-repeat="item in todos | filter: {complete: true}">
		...
	</li>

