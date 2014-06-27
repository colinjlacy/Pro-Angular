Two-way data binding is exactly what it sounds like, as compared to the one-way data binding that was looked at in the previous doc.  Instead of data being bound from the back end to the front end only, data is bound both ways.  A user can access data from the database, as well as input and modify that data instantly on the client level.  This can only be done, it should be noted, with input-type UX elements - `input`, `textarea`, and `select` elements.

To demonstrate, the following example shows how the two relate:

	<!-- prints the initial data found in $scope.somethingToDo -->
	<p>Today, you should {{somethingToDo}}.</p>

	<!-- anything put in here will be the new value of $scope.somethingToDo -->
	<input type="text" ng-model=somethingToDo placeholder="What do you want to do?" />

One of the initial demos of Angular shows how this can work even if the `$scope.somethingToDo` value was never initially set.  By binding data to an empty `$scope` property, you will still end up seeing that data displayed once it's populated by the input element.

Regardless of whether or not the bound data is empty, any changes made in a two-way `ng-model` binding will be automatically applied to any iterations of that data object.  So any one-way bindings will see an instant update, even as the user types into the input field.