### The JavaScript Event Loop

The simplest explanation of JavaScript's concurrency model uses two rules: If some JavaScript is running, let it run until it is finished ("run-to-completion"). If no JavaScript is running, run any pending event handlers.

Since most JavaScript is run in response to an event, this is known as an event loop: Pick up the next event, run its handler, and repeat.

There are three parts you have to think about around the event loop:

    the Call Stack
    Web APIs/the browser
    an Event Queue

Not all of the code that we write is 100% JavaScript code. Some of the code is interacting with the Web APIs (also known as "browser APIs"). There are many more examples, but both .addEventListener() and setTimeout() are Web APIs.

Let's look back at this code:

    console.log('howdy'); // 1
    document.addEventListener('click', // 2
    function numbers() {
        console.log('123');
    });
    console.log('ice cream is tasty'); // 3

First, the browser runs this block of code to completion -- that is, steps 1, 2, and 3. Step 2 passes an event handler (numbers) to the browser for future use: the browser will hold this function until there's a click event.

What happens if someone clicks before this block of code is done? When there is a click event and there is code already running, the numbers function can't just be added directly to the Call Stack because of JavaScript's run-to-completion nature; we can't interrupt any code that might currently be happening. So the function is placed in the Queue. When all of the functions in the Call Stack have finished (also known as idle time), then the Queue is checked to see if anything is waiting. If something is in the Queue, then it's run, creating an entry on the call stack.

IMPORTANT: The key things to remember here are 1) current synchronous code runs to completion, and 2) events are processed when the browser isn't busy. Asynchronous code (such as loading an image) runs outside of this loop and sends an event when it is done.

What is the order that the iceCream function goes through if the <footer> is clicked?
    const pageFooter = document.querySelector('#page-footer');

    pageFooter.addEventListener('click', function iceCream () {
        const footerDetails = document.querySelector('#details');

        footerDetails.textContent = 'Everyone should eat ice cream!';
    });

First   Browser

Second  the Queue

Third   the Call Stack

