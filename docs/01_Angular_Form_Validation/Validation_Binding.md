If you're looking to connect the functionality/operability of an element to the validity of a form, then you'll look to the properties of the form object.  Angular automatically adds properties that define validity for the form object, which can be accessed on the `$scope`.

The following will be set to true (and therefor will return true when passed to an `ng-show`) if any element of the form is invalid:

    myForm.$invalid

With that in mind, I can set a submit button to be disabled when the form is invalid by adding the `ng-disabled` attribute:

    <input type="submit" ng-disabled="myform.$invalid" />
