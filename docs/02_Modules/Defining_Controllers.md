Controllers are essential to Angular as they provide access between the model and view of the app.  Most apps have multiple controllers, each of which delivers data logic for one aspect of the app.

Controllers are defined using the `Module.controller` method, which takes two arguments:

1. the name of the controller
2. the factory function used to set up the controller and get it ready for use

It's considered a common naming convention to append the suffix "Ctrl" to the name of the controller.

Within the factory function, the arguments passed are the dependencies used to get the controller up and running.  Common dependencies seen in even the most basic apps are the Angular services `$scope`, and `$http`. This is known as *dependency injection*.

##Understanding Dependency Injection##

When declaring a controller, Angular sees the arguments passed to the factory function, and then searches throughout the app for the components/services declared in those arguments.  The problem this seeks to solve is to allow developers to use and select key services that are essential to executing the code within the controller they are defining without having to resort to global variables.

Once a dependency is declared as an argument of the controller's factory function, Angular knows to go look for it and pass access to its properties/methods to the controller being declared.  That helps keep the global scope clean, while allowing access to be shared between various parts of the application.

The interesting thing about dependency injection is that it works in the opposite form of most arguments passed to functions.  Normally, when you pas an argument, you expect to treat the argument as data *received* by a function.  In the case of DI, the function is commanded to go looking for the components in the grand scheme of the Angular app - to demand access to each argument's properties, if you will.

##Applying Controllers to Views##

Once a controller has been declared, it needs to be bound to an HTML element in order to manipulate the view with any data it receives.  This is done with the `ng-controller` attribute.

	<div class="panel" ng-controller="myCtrl">

Anything inside that `<div>` is now the view in the MVC framework, accessed by the controller.

The `$scope` used in declaring the controller is the component that binds data to the view.  Only data passed to the `$scope` can be bound.

##Creating Multiple Views##

Each controller can support multiple views, which allows the same data to be presented in different ways, or for closely related data to be created and managed efficiently.  It's not complicated; simply declare the same controller on multiple elements' `ng-controller` attributes.

	<div id="first-div" ng-controller="myCtrl">

	<!-- some content... -->

	<div id="eigth-div" ng-controller="myCtrl">

This way, you can access the same data in mulitple places, or access data that's processed in the same way multiple places.  When the data is drastically different, you'll want to move it into a second controller.

##Creating Multiple Controllers##

Creating a second or more controllers works the same way as creating the first controller.  There are just some caveats to keep in mind when doing so.

First of all, each controller has to be brought into the application with a `<script>` tag in the head of the application.

Second, each controller has its own piece of the `$scope`.  So you can actually define the same `$scope` property name in two different controllers, and there will be no conflict.  Consider the `$scope` of each controller to be a local declaration.