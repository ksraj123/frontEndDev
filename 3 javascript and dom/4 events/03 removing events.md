### Object equality in javascript

Two objects are equal in javascript only when they point to the same instance.
    { name: 'Saurabh' } === { name: 'Saurabh' } // false
    { name: 'Saurabh' } == { name: 'Saurabh' } // false

    var jangoFett = {occupation: "Bounty Hunter", genetics: "superb"
    };
    var bobaFett = {occupation: "Bounty Hunter", genetics: "superb"
    };
    var callMeJango = jangoFett;
    // Outputs: false
    console.log(bobaFett === jangoFett);
    // Outputs: true
    console.log(callMeJango === jangoFett);

Infact object variables are nothing but references in javascript, take a look at this
    const obj = {value: 10}
    obj.value = 20
    consle.log(obj); // {value: 20}
    obj = {name: "Saurabh"}; // TypeError: assignment to const

A `const` object means that it will keep pointing to the same object in memory but that object itself can be modified.

    (undefined == undefined) // true
    (undefined === undefined) // true
    (NaN == NaN) //false
    (NaN === NaN) //false

if we really want to compare the values within two objects then we can iterate the two objects and compare each value
but that would also not work well if the values themselves are other objects or NaN

so check if two objects are the equal by value the best way is to use a third party library like [underscore](https://underscorejs.org/)

    _.isEqual(object1, object2)


now looks at this code

    var a = {
        myFunction: function quiz() { console.log('hi'); }
    };
    var b = {
        myFunction: function quiz() { console.log('hi'); }
    };
    a.myFunction === b.myFunction

what would this code result in? It would result in false.
In JavaScript, functions are first-class objects, because they can have properties and methods just like any other object.

    function quiz() { ... }

    var a = {
        myFunction: quiz
    };
    var b = {
        myFunction: quiz
    }
    a.myFunction === b.myFunction       // true

okey so why do we care about object equality when removing events?

To remove an event this is the syntax for `removeEventListener` method:-
    <event-target>.removeEventListener(<event-to-listen-for>, <function-to-remove>);

So function here shold not just be the same looking, it should be the instance of the original function which was passed to `addEventListener`

This is how it should be used as

    function myEventListeningFunction() {
        console.log('howdy');
    }

    // adds a listener for clicks, to run the `myEventListeningFunction` function
    document.addEventListener('click', myEventListeningFunction);

    // immediately removes the click listener that should run the `myEventListeningFunction` function
    document.removeEventListener('click', myEventListeningFunction);

Now have a look at the below code:

    myForm.addEventListener('submit', function respondToSubmit(){...});
    myForm.removeEventListener('submit', function respondToSubmit(){...});

Here the listener will not be removed and the element will still have an event listener