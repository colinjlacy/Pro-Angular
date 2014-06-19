This is one of the most basic directives in AngularJS, but also one of the most powerful.  It loops through items in an array bound to the `$scope`.  So for example, if I have a products array, I can loop through each one and display it's different properties.

    <li ng-repeat="item in products">
        {{item.name}} <em>{{item.price}}</em
    </li>

Obviously this can get a lot more complicated.  But one fun thing about `ng-repeat` is that it keeps in line with data binding.  So if the amount of items in the array changes, the element with the `ng-repeat` directive will append or pull to/from the array automatically.

##Built-in variables##

`ng-repeat` comes with some built-in variables that can tell me something about each item as it is populated.

* `$index` - returns the position of the element in question within the array.  Can use this to map back to elements in other arrays.
