What might seem at first like a simple way to plug data into the database can actually turn out to be one of the more sophisticated aspects of Angular, allowing some serious CRUD and giving users the ability to really futz with data however they like.

In the initial sense, `ng-model` can be used for some simple rabbit-out-of-hat trickery:

    <input ng-model="displayValue" type="text" />
    <p>{{displayValue}}</p>

The above is the most readily accessible example of how freaking cool Angular is at first glance.  

However, you can get more complicated by binding `ng-model` to data defined in a `.js` file, or data pulled from a database.

A perfect example for when to do this is when updating a database entry, for example, a product in an e-commerce shop.  

Without walking through the code (see **Pro Angular** for examples), think about it this way.

1. You have an array of products, which you display in a table.
2. When you click an *edit* button, the data for a certain product is passed to an object in the `$scope`.
3. You have a set of input fields that are bound to that `$scope.object`, using ng-model (e.g. `ng-model="object.price"`).
4. Because the inputs are bound to that data, they are pre-filled with the properties of the product object.
5. Edit any of the fields, and then click *save* to activate a function that makes an HTTP call to an API, updating that product via POST.

It's a lot of code, otherwise I would include it all here.  But it works!
