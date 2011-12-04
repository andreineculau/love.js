# Intro/Disclaimer
This document is not trying to set right from wrong.  
At least not for the whole world. But just for my case.  
It is a mear try to be consistent.

Some references can be found at the bottom,  
otherwise you won't find arguments for the choices below.

# Style consistency

## Characters per line
Have 80 characters per line as a guideline, and enforce it.  
But if you have a long RegExp, or you go 85 on a line, then don't sweat about it.

## Whitespaces
No tabs allowed.  
4 spaces indentation.  
No whitespace at the end of the line and no lines with only whitespaces.  
Use no more than 1 empty line to make code more readible.

## Brackets (round, square, curly)
Braces should be surrounded by whitespace,  
except when enclosed by other brackets or when used for function's arguments.

## Braces (curly brackets)
Same lines braces.  
Use braces even with single line blocks.

    // YES
    if (true) {
      alert({a: 'a'});
    }

    // NO
    if (true)
      alert( {a: 'a'});
    if (true){
      alert( {a: 'a'});
    }
    if (true)
    {
      alert( {a: 'a'});
    }

## Object definition braces
An object that cannot be defined inline, will be defined after a breaking brace,  
with the closing brace on a line of its own.

    // YES
    a = {b: 'b'};
    c = {
        d: 'd',
        e: 'e'
    };

    // NO
    c = {d: 'd',
        e: 'e'};

## Readable keywords and operators
Always surround them by whitespace, except for a function definition and call.

    // YES
    a = function(x) {...};
    b = a(2);
    c = a(3);
    d = (b || c) && true;

    // NO
    a = function ( x ) {};
    b = a (2);
    c = a( 3 );
    d = (b||c)&&true;

## Breaking operators
An expression that cannot be written inline, will be broken after an operator.

    // YES
    a = a &&
        (b || c);

    // NO
    a = a && (
        b || c);

## Breaking comma and semicolon
Comma and semicolon are followed by a whitespace or new line.  
They always come last, never start a new line with one.

## var
Declare your variables at the top of your code, except for function expressions.  
Try to Use one line per variable, but you're the better judge.  
For consistency, leave the keyword var on its own line.

    // YES
    var
    a,
    b = 5;

    // NO
    var a,
        b = 5;
    var a;
    var b = 5;

## Single quotes vs double quotes
Use single quotes.  
If you have an English 'I'm' then just escape it: 'I\'m'.  
If you have plenty of escapings, then decide yourself if you want to switch  
to double quotes: "I'm ready, ma'am!".

## Semicolons
Always use semicolons.

    // YES
    x = x + 1;
    return x;

    // NO
    x = x + 1
    return x

## Readable arithmetics
Instead of 86400000 (a day in miliseconds),  
break it down to 24 * 60 * 60 * 1000.  
Stop using ++i. Keep to i++, or even i = i + 1.

## Naming convention
underscore. Take it or leave it!  
~ "It is no measure of health to be well adjusted to a profoundly sick society."

Make use of prefixes (eg. has_, is_) and suffixes (eg. _count)

Functions (which should always be function expressions) and variables will use  
lowercase underscore notation.  
Classes are capitalized, and constants are uppercase.

    // YES
    var always_underscore = new Base_class();
    var always_and_forever = function() {...};
    CONST_VALUE = 10;

# Now code!
## "use strict" and use JShint/JSlint

## Global namespace
The less global variables, the better. Your goal should be 0.

    // YES
    (function() {
      var a = 2;
      var b =
    })();

## Comparisons
Always use the === equality and !== inequality operators.  
You can use == only when checking against null.

    // YES
    if (a === '1') {...}

    // NO
    if (a == 1) {...}
    if (a) {...}

## else, else if, catch
"else" "else if", or "catch(e)" will stay on the same line  
with the closing and the opening brace.

## Loops
If order doesn't matter, just parse in reverse with a while loop.  
Otherwise, just declare variables before the for loop.

    // YES
    var
    i, l;
    for (i = 0, l = 100; i < l; i++) {...}

    // YES
    var
    l = 1000;
    while (l--) {...}

    // NO
    for (var...) {...}
    for (i = 0; i < s.length; i++) {...}

## DOM repaints
Try to change the DOM as few as possible  
(eg. build the whole HTML before inserting it).

    // YES
    a = '<br>';
    while (b) {
        a += '<br>';
    }
    c.innerHTML = a

    // NO
    while (b) {
        c.innerHTML += '<br>';
    }

## Type checks
String: typeof object === 'string'  
Number: typeof object === 'number'  
Boolean: typeof object === 'boolean'  
Object: typeof object === 'object'  
Function: typof object === 'function' or better jQuery.isFunction(object)  
Array: object instanceof Array or better jQuery.isArray(object)  
Element: object.nodeType  
null: object === null  
null or undefined: object == null  
undefined: typeof variable === "undefined"  
existance "variable" in object

## RegExp
No more 'string'.match().  
Use only RE.test() and RE.exec().

## Libraries/frameworks
* [underscore.js](https://github.com/documentcloud/underscore)
* [jQuery](http://github/jquery/jquery)
* [JSON](https://github.com/douglascrockford/JSON-js)
* ...

# Document and don't comment!
Never document obvious code. It will make your work even more unreadable.  
Always try to make your code readable, rather than using lots of comments.  
So either go with JSDoc or with single line comments. No /*...*/

## JSDoc
### Functions
Each function should have a JSDoc heading.  
// TODO

### Variables
Decide on an individual basis for variables.  
// TODO

# References
http://taitems.github.com/Front-End-Development-Guidelines/ v  
http://www.youtube.com/watch?v=cIOIyfRoGcM

http://eloquentjavascript.net/contents.html  
http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml  
http://docs.jquery.com/JQuery_Core_Style_Guidelines v  
http://dmitrysoshnikov.com/ecmascript/javascript-the-core/  
http://bonsaiden.github.com/JavaScript-Garden/  
http://james.padolsey.com/javascript/terse-javascript-101-part-1/  
http://james.padolsey.com/javascript/terse-javascript-101-part-2/  
http://www.developer.nokia.com/Community/Wiki/JavaScript_Performance_Best_Practices

http://blog.codylindley.com/links

http://net.tutsplus.com/tutorials/javascript-ajax/24-javascript-best-practices-for-beginners/  
https://github.com/rwldrn/idiomatic.js  
http://dev.opera.com/articles/view/efficient-javascript/

http://mislav.uniqpath.com/2010/05/semicolons/ v  
http://whathecode.wordpress.com/2011/02/10/camelcase-vs-underscores-scientific-showdown/ v  
http://www.koonsolo.com/news/dewitters-tao-of-coding/ v
