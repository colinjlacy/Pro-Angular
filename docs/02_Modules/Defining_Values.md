Values are standardized, fixed values and objects that are applied to an application module.  They are created the same way as - and are, essentially - services; but their returned or declared values remain fixed to the app.  This is essentially the same as declaring global variables, but in an Angular way.

	myApp.value("developer", "Colin!");

	myApp.value("today", new Date());

	myApp.value("wife", {name: "Ashley", hot: true});

The major benefit of using them is that they are standardized across your application. Once they're set, they remain set on the global scope, but can then be worked with in the scope of a controller or service. If you need to change a value, you only have to do it once.  You also don't run the risk of overwriting or conflicting, as you would with a plain vanilla global JavaScript variable.