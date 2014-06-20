A module doesn't have to be an entire application.  It can actually just be a part of an application, broken out into a separate bit that can be called by other modules, and other applications.  That's what makes them modular.

For example, let's say I want to make a module that houses my controllers. I can do that.

	var controllersModule = angular.module("myApp.Controllers", []);

	controllersModule.controller("thisCtrl", function($scope, $http) {
		// do some of the things...
	});

	controllersModule.controller("thatCtrl", function($filter) {
		// do the rest of the things...
	}

I can also do this with filters, services, etc.

	angular.module("myApp.theFilter", [])
		.filter("filteringStuff", function() {
			// filter the things...
		});

It's worth noting that if a module is specifically going to be used in one app, or for one other module, it's good naming convention to append that module name to the name of the module you're creating.  Almost as if the name string were actually demonstrating an object-property relationship between the importing module, and the module being created.

Once declared and save - literally - wherever, there are two steps to pulling these modules into an app.

The first is to call the file in a `<script>` tag, the same way you would with any other JavaScript.  This has to happen after you pull in your `angular.js` file, but can happen in any order after that.

	<script src="angular.js"></script>
	<script src="controllers.js"></script>
	<script src="filters.js"></script>

The second is to mark the name of that module in the requirements (or dependencies, if you will) list for the module that's doing the importing.

	var myApp = angular.module("myApp", [
		'myApp.Controllers',
		'myApp.theFilter'
	]

It's worth pointing out that modules can be written and saved literally anywhere, and so sometimes you'll find two or more piled into the same file, especially if they are related.  Thinking in terms of efficiency, less HTTP requests technically means better performance.  So that.

Once it's pulled in as a dependency, a module behaves the same as it would if it were defined within the module calling it.  Its properties (controllers, filters, values, etc.) become the calling module's properties.  There's no need to specify the name of the module when accessing its properties.  There's also no need to consider ordering when creating the dependencies list.  It's all good.

The fun part is that there is no right answer as to how to structure modules.  So a module can be comprised of controllers and filters, services and values, controllers and constants, or whatever. Go nuts!
