There are now two new ways to declare variables in JavaScript: **let** and **const**.

### need for `let` and `const`

consider the following code below -

    function getClothing(isCold) {
      if (isCold) {
        var freezing = 'Grab a jacket!';
      } else {
        var hot = 'It’s a shorts kind of day.';
        console.log(freezing);
      }
    }


    getClothing(false);
one might think that the output of this code is `Reference Error: freezing is not defined` but actually it is undefined.
The reason for that is **Hoisting**

### Hoisting

Any JavaScript code is executed, all variables declared with var are "hoisted", which means they're raised to the top of the function scope.

so our previous `getClothing` function actually looks like this

    function getClothing(isCold) {
      var freezing, hot;
      if (isCold) {
        freezing = 'Grab a jacket!';
      } else {
        hot = 'It’s a shorts kind of day.';
        console.log(freezing);
      }
    }

### let and const

Variables declared with let and const eliminate this specific issue of hoisting because they’re scoped to the block, not to the function. Previously, when you used var, variables were either scoped globally or locally to an entire function scope.

If a variable is declared using let or const inside a block of code (denoted by curly braces { }), then the variable is stuck in what is known as the temporal dead zone until the variable’s declaration is processed. This behavior prevents variables from being accessed only until after they’ve been declared.

    function getClothing(isCold) {
      if (isCold) {
        const freezing = 'Grab a jacket!';
      } else {
        const hot = 'It’s a shorts kind of day.';
        console.log(freezing);
      }
    }

    getClothing(false);

Now upon execution it will work like we initially expected and give `Reference error`