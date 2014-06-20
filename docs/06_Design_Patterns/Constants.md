You can define constants that will be used with each controller, whcih can run data throughout the controller without having to repeat yourself.  In **Pro Angular**, the most common uses of constants are for API URLs.  

    angular.module("myApp")
        .constant("theUrl", "http://someurl.com/endpoint/")
        .controller("myController", function($http, theUrl) {
            ...
            })

Notice that I had to pull it into the controller the same way I would with any other service that a controller depends upon.  This might suggest that I can define constants anywhere throughout the application.
