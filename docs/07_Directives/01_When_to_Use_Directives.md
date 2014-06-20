Angular treats HTML elements with love and respect, and uses directives to build on standard semantic HTML elements and attributes.  Consider this a stark contrast to other libraries like jQuery, which - arguably - treat elements like obstacles to be overcome.

Directives apply core Angular features like DOM manipulation and validation directly to HTML elements, rather than producing results in the background and injecting/bootstrapping/hacking them into the DOM once they've been constructed.  Think of how `ng-repeat` calls a loop directly on the HTML element, rather than creating a `$.each()` loop to build an HTML block and pushing it into an unassuming `<ul>` with a `$('ul').html()` call.

As for the top-level question of when to use directives - whenever possible is the answer.