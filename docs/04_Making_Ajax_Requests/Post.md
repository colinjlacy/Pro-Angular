Post is used to insert data into a database, usually via an API.  When using post, you tend to insert a data object into a database, with the properties of the data object matching the column labels of the database.  So, for example, if I were to have a database with the following structure:

* first_name, string
* last_name, string
* address, string
* birthday, string
* age, int
* sexy, bool
* hobbies, array

I would want my data object to fall in line with a matching set of properties, defined in such a way that they would fit smoothly into the database:

    var data = {
        first_name: "Colin",
        last_name: "Lacy",
        address: "232 Fried",
        birthday: "July 21",
        age: 29,
        sexy: true,
        hobbies: [
            boxing,
            coding,
            sleeping,
            eating
        ]
    }

If, for example, the database were looking for an integer, or a boolean for one of its columns, I'd want to make sure my data object has that data-type in the corresponding property.  Note how the last three columns of the database structure at the top of the page correspond to the data-types of the last three properties of the data object.

Once we've defined a data object, we can start to look at sending it off to the database by defining a URL to which we can pass our request.

    var theUrl = 'http://somewebsite.com/database/';

Now that that bit is done, we can pas the data either as a post method of the `$http` service object, or as a part of an `$http` object.

    // one option:

    $http.post(theUrl, data);

    // the other option:

    $http({
        url: theUrl,
        method: "POST",
        data: data
        });

    // a hybrid option, for the weirdos out there

    $http.post(theUrl, {
        prop: "value",
        otherProp: "other value"
        });

Just like with any HTTP request sent, the promise will be handled wither either a `success()` function call, or an `error()`.  In this case, the promise returns the data that was entered when it's successful.  So, if, for example, the database automatically creates an `id` value for the data object inserted, that will be returned (and accessible) as part of the data object.

    .success(function(data) {
        $scope.insertId = data.id;
        });

In a real-world scenario, this can be used as a reference to a calendar item when inserting something via the Google Calendar API.  It's also worth noting that because it returns the entire data item inserted, it comes back with any other properties the database automatically applies.  To continue with Google Calendar, that could be whether or not the current user created the event, whether or not it's set to recur, the iCal format of the event, etc.  Can be pretty useful.
