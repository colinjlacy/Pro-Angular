Forms in Angular come with built-in validation.  Once you give a form a name, Angular creates an object for it on the `$scope`, with its child input elements set as properties.  For example:

	<form name="myForm" novalidate>
		<input type="text" name="textInput"/>
		<input type="number" name="numberInput" />
	</form>

Will result in the object:

	myForm : {
		text: {}
		number: {}
	}

You'll notice that each input becomes an object when added as a property of the form object.  This is where validation and value evaluation are applied - in the properties of those input objects.  You can access their properties like so:

	form.text.someProperty

It's worth noticing the `novalidate` hanging out in the form element.  That prevents browsers and Bootstrap from working their own validation on the form element.  We don't want the user to get too many alert notices that they've done something wrong.

##Validation Classes##

Angular applies classes to form elements when they meet or fail certain validation requirements:
* `.ng-invalid`
* `.ng-valid`

You can anticipate these classes with careful CSS styles.  For example, you can set background colors, font-weights, and borders.  You can even target individual types of form elements for selective styling:

	input["type=text"].ng-invalid { background-color: @angry; }
