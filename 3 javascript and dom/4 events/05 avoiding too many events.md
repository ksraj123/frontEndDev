Consider this code below:

    const myCustomDiv = document.createElement('div');

    for (let i = 1; i <= 200; i++) {
        const newElement = document.createElement('p');
        newElement.textContent = 'This is paragraph number ' + i;

        newElement.addEventListener('click', function respondToTheClick() {
            console.log('A paragraph was clicked.');
        });

        myCustomDiv.appendChild(newElement);
    }

    document.body.appendChild(myCustomDiv);

In this code 200 `p` elements are created and all of those elementes will have a seperate eventListener associated to them and each will have a seperate function.

Since the function in each is doing the samething coz its the same function we can create one function and provide instances to it instead of creating new ones, this will save memory and increase performance

    const myCustomDiv = document.createElement('div');

    function respondToTheClick() {
        console.log('A paragraph was clicked.');
    }

    for (let i = 1; i <= 200; i++) {
        const newElement = document.createElement('p');
        newElement.textContent = 'This is paragraph number ' + i;

        newElement.addEventListener('click', respondToTheClick);

        myCustomDiv.appendChild(newElement);
    }

    document.body.appendChild(myCustomDiv);

Another great idea could be attach one event listener to the wrapping div instead of 200 event listeners to each individual paragraph and this would improve performace by a lot. To identify which paragraph eactly the user clicked on we could use the event.target property

### Event Delegation

The event object has a .target property. This property references the target of the event. Remember the capturing, at target, and bubbling phases?...these are coming back into play here, too!

Let's say that you click on a paragraph element. Here's roughly the process that happens:

    a paragraph element is clicked
    the event goes through the capturing phase
    it reaches the target
    it switches to the bubbling phase and starts going up the DOM tree
    when it hits the <div> element, it runs the listener function
    inside the listener function, event.target is the element that was clicked

So event.target gives us direct access to the paragraph element that was clicked. Because we have access to the element directly, we can access its .textContent, modify its styles, update the classes it has - we can do anything we want to it!

    const myCustomDiv = document.createElement('div');

    function respondToTheClick(evt) {
        console.log('A paragraph was clicked: ' + evt.target.textContent);
    }

    for (let i = 1; i <= 200; i++) {
        const newElement = document.createElement('p');
        newElement.textContent = 'This is paragraph number ' + i;

        myCustomDiv.appendChild(newElement);
    }

    document.body.appendChild(myCustomDiv);

    myCustomDiv.addEventListener('click', respondToTheClick);


**Note** - when useCapturing is set to true and we are listening for events on the parent element on which it is set true then also event.target works fine without any issue

**but there is an issue here,**

suppose that we have the following setup inside the paragraph
    <p>Paragraph 1 <span>testing</span></p>
and the user clicken on the testing part,
then the span will be the event.target and not the paragraph this would mess things up as we were expecting the paragraph to be the target in other parts of our code

to counter this we can use the `nodeName` property which is actially defined in the node interface but since the element interface inherits the node interface is is present in there too

the `nodeName` has all of its letters capitalised
so we can check in the event listener if the target is a paragraph of not

    if (event.target.nodeName === "P")

but the issue with this is not if we click on the span part then now then nothing happens, it is the part of the paragraph too so clicking on it should make stuff happen