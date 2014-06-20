Modules are the highest-level components of an Angular application.  They have three main roles in an Angular app:

* To associate AngularJS with a region of an HTML document
* To act as a gateway to key Angular framework features
* To help organize code and components in an Angular application

The first step to creating an AngularJS app is to define a module and associate it with a region of HTML:

	var myApp = angular.module("myApp", []);

The module method on the `angular` object supports three methods, although it's generally common to only use the first two:

1. `name` - the name of the module - in this case, "myApp"
2. `requires` - other modules that are required to run this module
3. `config` - the configuration for the module, when applicable (the same as calling the `Module.config` method)

As a naming convention, it's common to end the top-most level module with the suffix "App".  This can help make it stand out in an application with multiple modules.

Once it's define, it has to be bound to HTML content using the `ng-app` attribute.  When Angular is the only framework being used on the front end, it's common to apply it to the `html` element.

	<html ng-app="myApp">

It's worth noting that a `requires` argument is necessary in order to declare a module, and therefore can be an empty array `[]` if no dependencies exist.  Without any second argument passed, Angular will treat it like a module that has already been declared, and will break when that module can't be found.