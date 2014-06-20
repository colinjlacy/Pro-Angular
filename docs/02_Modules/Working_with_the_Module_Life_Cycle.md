There are two methods that call functions throughout the invocation of a module: `Module.config` and `Module.run`.

A function passed to the `.config` method is run when *the current* module has been loaded, and a function passed to the `.run` method is run when *all* modules have been loaded.

##Using `.config`##

First of all, it's worth noting that a `.config` call can gain access to a module's `Module.constant` properties. A constant is virtually the same as a value, but it can be accessed by the constant, while values cannot.  An example of this would be to set a base URL as a constant and then pass it to a config for things like customizing the property of an `$http` service within the module - i.e. declaring `withCredentials` on all HTTP requests.

 Generally speaking, you'll use `.config` to inject values that have been set manually, or obtained from the server, for use throughout the module.  Since it's run at the time the module is loaded, it will be instantiated before other modules are loaded.

##Using `.run`##

The run method also accepts a function, but will be run once the entire application is done loading.

##Callback Order##

Callbacks on dependencies are invoked before callbacks on the modules that depend on them.  So, let's say I have the following module:

	angular.module("topModule", [
		'lowerModule'
	]);

The order in which the callbacks will be executed is:

1. `lowerModule.config`
2. `topModule.config`
3. `lowerModule.run`
4. `topModule.run`


