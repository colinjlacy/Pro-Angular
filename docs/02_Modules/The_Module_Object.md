Once a module has been declared, it is instantiated as a new `Module` object, and comes with all of the properties and methods of the `Module` constructor:

* `animation(name, factory)`
* `config(callback)`
* `constant(key, value)`
* `controller(name, constructor)`
* `directive(name, factory)`
* `factory(name, provider)`
* `filter(name, factory)`
* `provider(name, type)`
* `name`
* `run(callback)`
* `service(name, constructor)`
* `value(name, value)`

These methods/properties can all be summed up into three broad categories:

1. those that define components for an Angular application
2. those that make it easier to create those building blocks
3. those that help manage the AngularJS life cycle.