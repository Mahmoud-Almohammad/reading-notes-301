# THE CALL STACK

A **call stack** is a mechanism for an interpreter (like the JavaScript interpreter in a web browser) to keep track of its place in a script that calls multiple functions — what function is currently being run and what functions are called from within that function, etc.

- When a script calls a function, the interpreter adds it to the call stack and then starts carrying out the function.

- Any functions that are called by that function are added to the call stack further up, and run where their calls are reached.

- When the current function is finished, the interpreter takes it off the stack and resumes execution where it left off in the last code listing.

- If the stack takes up more space than it was assigned, a "stack overflow" error is thrown.

## Example

    function greeting() {
    // [1] Some code here
    sayHi();
    // [2] Some code here
    }
    function sayHi() {
    return "Hi!";
    }

    // Invoke the `greeting` function
    greeting();

    // [3] Some code here

The code above would be executed like this:

1. Ignore all functions, until it reaches the `greeting()` function invocation.

2. Add the `greeting()` function to the call stack list.

3. Execute all lines of code inside the `greeting()` function.

4. Get to the `sayHi()` function invocation.

5. Add the `sayHi()` function to the call stack list.

6. Execute all lines of code inside the `sayHi()` function, until reaches its end.

7. Return execution to the line that invoked `sayHi()` and continue executing the rest of the `greeting()` function.

8. Delete the `sayHi()` function from our call stack list.

9. When everything inside the `greeting()` function has been executed, return to its invoking line to continue executing the rest of the JS code.

10. Delete the `greeting()` function from the call stack list.

In summary, then, we start with an empty Call Stack. Whenever we invoke a function, it is automatically added to the Call Stack. Once the function has executed all of its code, it is automatically removed from the Call Stack. Ultimately, the Stack is empty again.

## You can find the resource [here on MDN][1] or [here on freecodecamp by charles freeborn][2]

***

# JavaScript error messages && debugging

Most of your time as a developer is spent reading code followed by debugging that same code, most likely to be able to read it or solve an “unexpected feature” (which, joking aside, is more correctly known as a “bug”).

![image](https://miro.medium.com/v2/resize:fit:828/format:webp/1*LHpmsxV3f2znpxhuAFuIqA.png)

This is a sample of an error, the green is the overall error message, the light blue is to note if the error was properly handled, the brownish (dark yellow) is the type of error and the red is the call stack

## Types of error messages

### Reference errors

This is as simple as when you try to use a variable that is not yet declared you get this type os errors.

    console.log(foo) // Uncaught ReferenceError: foo is not defined

This is also a common thing when using const and let, they are hoisted like var and function but there is a time between the hoisting and being declared so when you try to access them a reference error occurs, the fact that this happens to let and const is called Temporal Dead Zone (TDZ).

    foo = 'Hello' // Uncaught ReferenceError: foo is not defined
    let foo

Whatever you are using (var, let or const) the fix is as simple has declaring the variable before any declaration is made.

    let foo;
    foo = 'Hello'

### Syntax errors

This occurs when you have something that cannot be parsed in terms of syntax, like when you try to parse an invalid object using JSON.parse.

    JSON.parse( {'foo': 'bar'} ) // Uncaught SyntaxError: Unexpected token o in JSON at position 1

This can be solved by just fixing the syntax, in this case the object should be a JSON.

    JSON.parse('{"foo":"bar"}')

### Range errors

Try to manipulate an object with some kind of length and give it an invalid length and this kind of errors will show up.

    var foo= []
    foo.length = foo.length -1 // Uncaught RangeError: Invalid array length

An array for instance cannot have a negative length, why would you mess with the array length? Some people use it to set an array to empty.

### Type errors

Like the name indicates, this types of errors show up when the types (number, string and so on) you are trying to use or access are incompatible, like accessing a property in an undefined type of variable.

    var foo = {}
    foo.bar // undefined
    foo.bar.baz // Uncaught TypeError: Cannot read property 'baz' of undefined

This is probably the most frequent error in JS, trying to access a property/method thinking that bar is of the type object when in reality, since it hasn’t been declared yet, it’s undefined which doesn’t have any baz available.

The fix is simple, just make sure that bar exists before trying to access it, either by creating bar or by checking for undefined.

    var foo = { bar: {} }
    foo.bar.baz // undefined but you avoid the error

or

    var foo = {}
    if (typeof foo.bar !== 'undefined') {
    foo.bar.baz // this will never be executed while bar does not exist
    }

## Debugging

![image](https://miro.medium.com/v2/resize:fit:828/format:webp/1*ByuRUFwh_Nul0ZOOx4QVRg.png)

To debug your JS code, the easiest and maybe the most common way its to simply console.log() the variables you want to check or, by using chrome developer tools, open your page with your JS code (press cmd+o in macOS or Ctrl+o in Windows) and choose your file to debug, click the line you wanna debug and refresh your page again (F5).

If the line you selected was run you will be able to see what has happened before that point and you can try and evaluate the next lines to check if everything is outputting what you are expecting.

Using Node.js with Visual Studio Code you can press the debug tab and add a configuration similar to this:

![image](https://miro.medium.com/v2/resize:fit:828/format:webp/1*q0ybXMtFlQdnXQuOUNRQSw.png)

You can run the debugger by pressing F5 or pressing the green play button.

## and WE done! if you want to read the full article, you can read it from [this link][3]

[1]: <https://developer.mozilla.org/en-US/docs/Glossary/Call_stack>
[2]: <https://www.freecodecamp.org/news/understanding-the-javascript-call-stack-861e41ae61d4>
[3]: <https://codeburst.io/javascript-error-messages-debugging-d23f84f0ae7c>
