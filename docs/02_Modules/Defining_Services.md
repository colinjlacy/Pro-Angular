Services are singleton objects that provide one-off functionality that you might want to use or re-use anywhere in your application. (Singleton means that only one instance of the object will be created, and shared between various parts of the app that need to use it). Angluar comes with plenty of built-in services, like `$http`, `$scope`, and `$filter`.

The service method takes two arguments - the name of the service, and the factory function that is called to create the service object.  It is passed by name as a dependency to any controller that wishes to use it.

	myApp.service("myService", function() {
		// do the things...
	});

	myApp.controller("thatCtrl, function($scope, myService) {
		// do more the things...
	});

The benefit of using services as opposed to sticking everything in the controller is that the results of the service can be used anywhere in the application.  That's not the case for controllers, which are restricted to their own scopes.