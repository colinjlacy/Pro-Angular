I like `ng-class`, though I have to admit I'm still a little shaky on how to use it. The goal is to be able to apply classes to an element based on Angular and JavaScript statements.  

One of the simplest examples is for use in `ng-repeat`.  Think og the many ways in which you can write up user feedback for navigation, indicating that the user is on a page that is accessible via a navigation object.  Can get hairy.  WP and Drupal add classes like `is-active-page` dynamically to a nav item.  In JS, it requires a long conditional that access the window.location and the `href` attribute of the nav item.

In Angular, it's far simpler with `ng-class`.  First we'll set up some sweet JavaScript:

    // set a variable on the scope to mark the current active item

    $scope.active;

    // create a function that passes a data object as the active value

    $scope.setActive = function(item) {
        $scope.active = item;
    }

    // now assemble an array through which we'll iterate

    $scope.items = [
        'this',
        'that',
        'those'
    ]

Now, in the view, we'll iterate through the array, and pass the clicked item to the `setActive()` method.

    <li ng-repeat="item in items">
        <a ng-click="setActive(item)" ng-class="{'active' : item == active}">{{item}} link</a>
    </li>

Once an `<a/>` is clicked, it will pass the item to the `active` property, and will add the propert class to the element in question.  
