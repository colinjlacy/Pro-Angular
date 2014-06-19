AJAX Requests are one of the most significant features of Angular that I've come across.  The concept of two-way data-binding is fun when applicable, but in a lot of use cases for information distribution, data generally goes one way - from the server to the user.

Angular makes AJAX requests remarkably easy with the built-in `$http` service.  To include it in a controller or service factory, simply add it to the parameters of the top level defining function:

    angular.module('myApp')
        .controller('myController', function($scope, $http) {
            // doing some stuff here..
        });

Once that has been declared, the `$http` service is accessible anywhere within the controller/service.

The request method can be declared in one of two ways:

1. declaring as a method of the `$http` service:

        $http.post(...)

2. declaring as a value of the `method` property when defining an `$http` object:

        $http({
            ...
            method: 'POST',
            ...
            });

When using the request method as a method of the $http service, you have access to the various parameters available to each method.  This can help make things simpler if values for those parameters have already been defined in string variables (such as a URL) or object variables (such as a data object to be sent).
