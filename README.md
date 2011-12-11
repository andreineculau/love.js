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
Use no more than 1 empty line to make code more readable.

## Brackets (round, square, curly)
Brackets should be surrounded by whitespace, except  
when enclosed by other brackets or  
when denoting the beginning of a function's arguments.

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
with the closing brace on a new line.

    // YES
    a = {b: 'b'};
    c = {
        d: 'd',
        e: 'e'
    };

    // NO
    c = {d: 'd',
        e: 'e'};

## Readable keywords, operators and function calling
Always surround them by whitespace, except  
for the keyword function and function calling (ie. no whitespace after it).

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
Try to use one line per variable, but you're the better judge.  
For alignment consistency, leave the keyword var on its own line.
Indent and linebreak in a useful / readable way.
Assignment in the same statement as variable declaration is sometimes more readable.

    // YES
    var
    a, b, c;

    b = 5

    // YES
    var
    a,
    b = 5,
    c;

    // YES
    var a,
        b = 5,
        c;

    // MAYBE
    var a, b, c;

    b = 5;

    // NO
    var a, b = 5, c; // (hard to spot the assignment)

    // NO
    var a;
    var b = 5;
    var c;

## Single quotes vs double quotes
Preferrably use single quotes.  
If you have an English 'I'm' then just escape it: 'I\'m'.  
If your string would need plenty of escaped single quotes,  
consider using double quotes: "I'm ready, ma'am!".  

## Semicolons
Always use semicolons.

    // YES
    x += 1;
    return x;

    // NO
    x = x + 1
    return x

## Readable arithmetics
Instead of 86400000 (a day in miliseconds),  
break it down to 24 * 60 * 60 * 1000.  
Stop using ++i. Keep to i++, i += 1 or even i = i + 1.

## Comparisons
Always use the === equality and !== inequality operators.  
You can use == only when checking against null.

    // YES
    if (a === '1') {...}

    // NO
    if (a == 1) {...}

    // MAYBE
    if (a) {...} // I love this, it's compact and readable, what's wrong with it? :) / Isak

## Operator precedence, return
Don't assume operator precedence, enforce it with round brackets.  
Even if you get it right, you are most definitely hindering readability.  
Also, when returning expressions,
make sure you wrap the expression with round brackets.

    // YES
    var a = a || (b ? 1 : (b || c));
    return (a && b);
    
    // NO
    var a = a || b ? 1 : b || c;
    return a && b;

## else, else if, catch
"else", "else if", or "catch(e)" will stay on the same line  
with the closing and the opening brace.

## Naming convention
<!-- I thought the majority vote so far was to use camelCase? / Isak -->
<!-- Klarna's guidelines might follow love.js 99%,
with some differences... Klarna vs "stubborn me".
We should definitely take note of these differences / Andrei -->
Variables and functions (which should always be function expressions) will use  
lowercase underscore notation. Take it or leave it!  
~ "It is no measure of health to be well adjusted to a profoundly sick society."

Make use of prefixes (eg. has\_, is\_) and suffixes (eg. \_count)

Constants are use uppercase underscore notation.  
Classes are capitalized and camelCased.

    // YES
    var always_underscore = new BaseClass();
    var always_and_forever = function() {...};
    var CONST_VALUE = 10;

# Now code!
## "use strict" and use JShint/JSlint

## Global namespace
The less global variables, the better. Your goal should be 0.

    // YES
    (function() {
      var a = 2;
      var b =
    })();

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
    <!-- Actually it doesn't seem to matter if you do it like this, as long as s.length is not changed in the loop.
    The browser probably optimizes for you, just like it does with i++. /Isak -->
    <!-- But you cannot rely on those optimizations, can you ?
    And what if you sddenly change s.length? You then need to modify your for construction? /Andrei-->

## DOM repaints
Try to change the DOM as few times as possible  
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
Use only RE.test() and RE.exec().  
No more String.prototype.match(), inconsistent and deprecated informally.

## Libraries/frameworks
* [underscore.js](https://github.com/documentcloud/underscore)
* [jQuery](http://github/jquery/jquery)
* [json2.js](https://github.com/douglascrockford/JSON-js/blob/master/json2.js)
* ...

# Document and don't comment!
Never document obvious code. It will make your work even more unreadable.  
Always try to make your code readable, rather than using lots of comments.  
So either go with JSDoc or with single line comments. No /*...*/

## JSDoc
### Functions
All public module functions must have a good JSDoc heading.  
A really tiny private function, or internal helper function in some other  
function, might omit the JSDoc heading, if the naming makes it self-documenting  
and additional comments would just be superfluous and clutter the code.

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
http://www.youtube.com/watch?v=taaEzHI9xyY
