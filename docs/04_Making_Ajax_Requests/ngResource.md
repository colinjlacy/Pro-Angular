The `$resource` service is built on top of the features offered by the `$http` service...

You can use the `$resource` service to create an access object that will be used by the `$http` service to make requests to the API.  

    $scope.thisResource = $resource(urlVar + ":prop", { prop: "@prop" });

The first argument passed defines the URL structure that will be used to make API calls.  The `:prop` acts as a variable that is defined by the map object passed as the second argument.  The key in the object is the variable that's being defined, and the value is a property of the data object that the resource is working with.  If the object has said property, it is appended to the URL string defined in `urlVar`.  This process defines the URLs and HTTP methods used to access APIs, meaning less AJAX calls using the `$http` service. (Note that they don't actually have to be named the same thing, e.g. `... ":id", {id: "@username"}`)

If no object is passed, `$resource` defaults back to the `urlVar` only.  Kind of a safe way of accessing data.

This can really come in handy for longer API URL strings, such as Google Calendar, which have multiple arguments being made throughout the URL.

The resulting access object from using the `$resource` service has the methods:
* `query`
* `get`
* `delete`
* `remove`
* `save`

All of these methods are used to obtain and operate on data retreived from the server.  Calling these methods triggers appropriate AJAX requests and performs the required operation.  **It's worth noting that the access object created by the `$resource` service doesn't automatically create an AJAX call.  It's up to the developer to attached a method to the end to execute the request for data.**
