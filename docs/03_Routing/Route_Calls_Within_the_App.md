Sometimes you want to redirect the user to another part of the app as part of a functional behavior of your view.  Let's say they've submitted a form, and you've validated it and pushed it to your database.  The next step is to take them to a screen that let's them know everything has been entered.

To do this, you'll need to include the `$location` module as a dependency of your controller or service factory.

    .controller('dataInsert', function($scope, $http, $location) {
            ... // this will be demonstrated in a second...
        });

This allows me to use the $location module that is built into angular to change the browser location (just like `window.location` does, for example).

In this example I'll add some data to a database, handle responses, then redirect the user to a confirmation page.

    .controller('dataInsert', function($scope, $http, $location) {
            $scope.sendData = function(formData) {
                var data = angular.copy(formData);

                $http.post({
                    url: "http://mydatabase.com",
                    data: data
                })
                    .success(function(data) {
                        $scope.returnedDate = data;
                    })
                    .error(function(error) {
                        $scope.returnedError = error;
                    })
                    .then(function() {
                        $location.path("/confirm-submission");
                    });
            };
        });
