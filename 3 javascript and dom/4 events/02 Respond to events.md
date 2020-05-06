### Event Target

Do you remember the Node Interface and the Element interface from the first lesson? Do you remember how the Element Interface is a descendant of the Node Interface, and therefore inherits all of Node's properties and methods?

Well there was one piece that I totally skipped over then but am addressing now. The Node Interface inherits from the EventTarget Interface.

    Event Target <----- Node <----- Element

    EventTarget is an interface implemented by objects that can receive events and may have listeners for them.

    Element, document, and window are the most common event targets, but other objects can be event targets too…

As you can see from the image above, the EventTarget is at the top of the chain. This means that it does not inherit any properties or methods from any other interfaces. However, every other interface inherits from it and therefore contain its properties and methods. This means that each of the following is an "event target";

- the document object
- a paragraph element
- a video element
- etc.

EventTarget Interface doesn't have any properties and only three methods! These methods are:

- .addEventListener()
- .removeEventListener()
- .dispatchEvent()

### Adding An Event Listener

`.addEventListener()` method will let us listen for events and respond to them!

    <event-target>.addEventListener(<event-to-listen-for>, <function-to-run-when-an-event-happens>);

So an event listener needs three things:

- an event target - this is called the target
- the type of event to listen for - this is called the type
- a function to run when the event occurs - this is called the listener

The `<event-target>` (i.e. the target) goes right back to what we just looked at: everything on the web is an event target (e.g. the document object, a `<p>` element, etc.).

The `<event-to-listen-for>` (i.e. the type) is the event we want to respond to. It could be a click, a double click, the pressing of a key on the keyboard, the scrolling of the mouse wheel, the submitting of a form...the list goes on!

The `<function-to-run-when-an-event-happens>` (i.e. the listener) is a function to run when the event actually occurs.

    const mainHeading = document.querySelector('h1');

    mainHeading.addEventListener('click', function () {
    console.log('The heading was clicked!');
    });

[list of all kind of events](https://developer.mozilla.org/en-US/docs/Web/Events)