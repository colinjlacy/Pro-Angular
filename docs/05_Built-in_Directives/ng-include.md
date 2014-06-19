This directive works like an `include()` or `@include` call in a typical scripting language.  

    <div ng-include="views/this.html"></div>

Or, even more fun, it can take a scope property as an argument.

    <div ng-include="{{view}}"></div>

So technically I can build a page by creating an array of include values, and looping through them using `ng-repeat`.  It's wonky, and probably not the best way, but it'll work.

Even more fun, it also accepts a statement within the attribute invokation that can determine the value passed to the include call.  For example, let's say we build these function in the controller:

    // first I create an array that both functions can access
    $scope.options = [
        "this",
        "that",
        "those"
    ];

    // after that, I set a default include
    $scope.current = $scope.options[0];

    // then I create a function that will set the include
    $scope.setInclude = function(index) {
        $scope.current = $scope.options[index];
    };

    // next I create a statement that will define the include
    $scope.getIncludes = function() {
        return "views/" + $scope.current + ".html";
    };

I could then come back and write a template that calls the include based on some interaction from the user.

    <!-- loops through the options -->
    <li ng-repeat="option in options">
        <a ng-click="setInclude(option.$index)">{{option}}</a>
    </li>

    <!-- calls the include -->
    <div ng-include="getInclude()"></div>

Essentially what that does is sets a `$scope` property based on the option clicked in the `a` element, and pulls an HTML template into the include based on the `getInclude()` method.

While in most cases, you'll want to declare a view based on `ng-view`, that directive comes with limitations.  There can only be one view called in `ng-view` in a page, and there are plenty of cases where you'll need to provide views within views based on whatever the user is doing.
