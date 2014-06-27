While data-binding is the surface-level magic that makes Angular so attractive, the practical use of data-binding stops short once you start to apply it to real-world needs.  Apps of any sort need to be able to display different views depending on the data model being shown, and as a result we have a slew of template-based directives to work with, which help put logic into view templates without having to write complicated JavaScript; or in some cases, any JavaScript at all.

##Generating Elements Repeatedly##

One of the most common tasks when working with data is to loop through all of the items in an array and present them to a user in a repeating format.  For example, through a list, using a series of `<li>` tags.

Applying `ng-repeat` to an element automatically repeats that element and any nested child elements it might have, for the loop passed to the `ng-repeat` directive:

	<ul>
		<li ng-repeat="item in array">
			{{item.property}}
		</li>
	</ul>

The above markup will loop through the `$scope.array` source data array and print whatever value is in the `property` property of each item in the array.  The directive takes a variable type of approach (kind of like a for-as loop in PHP), where you assign each iteration of the array loop to a variable string, in this case `item`.  So each loop through the array assigns the next object in the array to `item`.  You can really use any variable name you want.

###Repeating for Object Properties###

It I want to also loop through each property in an object, I can do that as well.  It works along the same lines, and Angular is smart enough to figure out what I'm looking for as, instead of looping trough an array, it's looping through an object.

	<tbody>
        <tr ng-repeat="item in array">
            <td ng-repeat="prop in item">
                {{prop}}
            </td>
        </tr>
    </tbody>

##Repeating through Data Object Keys##

Another way to present a repeating loop is to have the `ng-repeat` directive return a value along with its key.

	...
        <tr ng-repeat="item in array">
            <td ng-repeat="(key, value) in item">
                {{key}} = {{value}}
            </td>
        </tr>
	...

##Built-In Variables##

One of the handiest variables built into the `ng-repeat` directive is the `$index` variable, which returns the item's position in the loop.  Keep in mind that it remains true to the data rules of array indices, so it starts at 0.  If you're iterating through a list and want the first number to be displayed as 1, second as 2, and so on, be sure to express the relative index as `{{$index +1}}`.

 One of the best ways to use `$index`, in my humble, is to pass its value to a function that will utilize its position in the loop for some sort of interaction, like removing an item from a list.  Here's one real-world example:

In my controller I say:

        $scope.remove = function(index) {
            $scope.add.items.splice(index, 1);
        };

Then in the template file, I say:

        <li ng-repeat="item in add.items track by $index">
            {{item}}
            <button class="pull-right btn btn-sm btn-danger fa fa-trash-o" ng-click="remove($index)"></button>
        </li>

The key item is the `<button>` element, which has the `ng-click` directive bound to it.  I pass the `$index` variable, and in return, I get a list without the item that I clicked on.  Neat!

###Tracking by `$index`###

By default, `ng-repeat` iterates over the values in the array.  So what that means is each value in array is treated as its own special object. If there are duplicates, `ng-repeat` breaks - because how can something be its own special thing if there are two of it?  The example above is one such case, where the list in question was to be a grocery list created by users.  You can't guarantee that they won't enter in the same thing twice, and so you can't have your app self-destructing every time they do.  The result is the `track by` extension of `ng-repeat`, which can point the directive to any property of the items in the loop and set that as the iterated property.  In this case, it was `$index`, as there's never going to be two of the same index in an array.

###Other Built-in Variables###

While not as sexy as `$index`, there are other variables that can be useful in how data is handled in a loop:

* `$first` - returns true if the object is first in the loop
* `$last` - returns true if the object is last in the loop
* `$middle` - returns true if the object is neither first, nor last
* `$even` - returns true if the object is among the even-numbered indices
* `$odd` - returns true if the object is among the odd-numbered indices

Here's an example that will strip a table based on the `ng-class` directive, and how it responds to a ternary expression that evaluates the `$odd` variable for an item in a loop:

		<tr ng-repeat="item in todos" ng-class="$odd ? 'odd' : 'even'">
            <td>{{item}}</td>
        </tr>

So if `$odd` returns true, then `ng-class` will bind the `.odd` class to the `<tr>`.  If false, it'll be `.even`.

##Repeating Multiple Scope-Level Elements##

By default, `ng-repeat` only iterates over one property of a data object.  There are times, though, when you need to iterate over multiple top-level properties for a data-object.  Let's say, for example, you need to create an element in the same hierarchical level for each property of each data-object being processed.  Hard to do without breaking something.  Thus the `ng-repeat-start` and `ng-repeat-end` directives.

This is an example you might find when creating a blog feed:

	<h3 ng-repeat-start="item in items">
		{{item.name}}
	</h3>
	<em>
		{{item.date}}
	</em>
	<p ng-repeat-end>
		{{item.snippet}}
	</p>

Notice that the `ng-repeat-end` directive goes on the last element in the loop.  This creates a sweet block of code that will be repeated for each `item in items` without having to wrap the repeated block in an element, just for the loop.