Angular is able to construct some simple form validation based on attributes on form elements.  The most simple is `required`.

	<input class="form-control" name="inputName" type="text" ng-model="data.model" required/>
	
##Error Handling##

When a form element that has been labeled `required` is empty, Angular adds a `required` property to the `$error` property object to that form element object.  You can test for `required` validation by setting a conditional to show only when the `$error.required` property is set:

	<span class="alert alert-danger" ng-show="myForm.name.$error.required">Please Enter a Name</span>
	
Note that this will be hidden until the `$error.required` property has been applied and returns true