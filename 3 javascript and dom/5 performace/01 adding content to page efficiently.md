Lets look at the following code below 

    for (let i = 1; i <= 200; i++) {
        const newElement = document.createElement('p');
        newElement.textContent = 'This is paragraph number ' + i;

        document.body.appendChild(newElement);
    }

so what this does is that it creates a new paragraph element and it adds text to it and then adds that paragraph elements to the body in every itheration

There is another more efficient way to do this

    const myCustomDiv = document.createElement('div');

    for (let i = 1; i <= 200; i++) {
    const newElement = document.createElement('p');
    newElement.innerText = 'This is paragraph number ' + i;

    myCustomDiv.appendChild(newElement);
    }

    document.body.appendChild(myCustomDiv);

The browser is constantly working to make the screen match the DOM. When we add a new element, the browser has to run through a reflow calculation (to determine the new screen layout) and then repaint the screen. This takes time.

If we had added each new paragraph to the body element, then the code would've been a lot slower, because this would cause the browser to go through the reflow and repaint process for each paragraph. 

### Testing Code Performance
We create a new div which is not in the DOM and we add all the paragraphs in every iteration to that div and then we add the div at once to the body

The standard way to measure how long it takes code to run is by using performance.now(). performance.now() returns a timestamp that is measured in milliseconds, so it's extremely accurate.

If you've ever used a timing procedure in another programming language, then you might've heard of Epoch time (also called Unix time or POSIX time). These tools tell you the time that has passed since 1/1/1970 (the first of January). The browser's performance.now() method is slightly different in that it starts measuring from the time the page loaded.

The following code below demonstrates how we use to measure performance

    const startingTime = performance.now();

    for (let i = 1; i <= 100; i++) { 
    for (let j = 1; j <= 100; j++) {
        console.log('i and j are ', i, j);
    }
    }

    const endingTime = performance.now();
    console.log('This code took ' + (endingTime - startingTime) + ' milliseconds.');

### Document Fragment

what if we want to add the paragraphs in the pervious example efficiently but we do not want and unnecessary extra div in our html? Document Fragment comes to the rescue,

    const fragment = document.createDocumentFragment();  // ← uses a DocumentFragment instead of a <div>

    for (let i = 0; i < 200; i++) {
        const newElement = document.createElement('p');
        newElement.innerText = 'This is paragraph number ' + i;

        fragment.appendChild(newElement);
    }

    document.body.appendChild(fragment); // reflow and repaint here -- once!

