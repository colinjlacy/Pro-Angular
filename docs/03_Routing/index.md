Routing plays a significant role in AngularJS, and the way in which a route is handled will define which view and which behaviors the app will have.

To define a route in an app, the first thing to do is include the route declaration in the app's dependencies:

    angular.module("myApp", [
        'ngRoute'
    ])
    ...

This will give the app access to the properties of the routing module.

Next, we'll start defining routes and behaviors as properties of the `$routeProvider` object that comes built into `ngRoute`.

    // note that in this example I'm continugin the block above.  This can be added separately if needed, in a separate .js file.
    ...
    .config(function($routeProvider) {
        $routeProvider.when("/this-url", {
            templateUrl: "/views/this-view.html",
            controller: "thisController"
            });
        $routeProvider.when("/that-url", {
            templateUrl: "/views/that-view.html"
            });
        $routeProvider.when("/not-what-i-want", {
            redirectTo: "/this-url"
            });
        $routeProvider.otherwise({
            templateUrl: "/views/that-view.html"
            })
        });

There is a solid overview of all of the possible uses for `$routeProvider` at the [AngularJS API Reference](https://docs.angularjs.org/api/ngRoute/provider/$routeProvider).
