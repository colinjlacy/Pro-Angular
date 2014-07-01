There are times when you're waiting for your complex app to load, when you'll see the inline binding expressions `{{...}}`.  This is the result of the HTML in the template loading before Angular gets to process it.  Note that this is rare in desktop browsers, and even most modern devices.  This generally happens with slower devices only.

	<div ng-cloak>
		{{some.binding}}
	</div>

Note that this will hide whatever element you've applied the attribute to, as well as anything inside of it.  So you can technically apply it to the `body` tag.  However just know that whatever is cloaked will not be visible, so if applied to `body` the user will see a blank screen while they wait.