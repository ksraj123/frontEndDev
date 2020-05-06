### Why we need events?
If we wrote everything in the javascript file directly then those changes whould be made imideately as soon as the javascript file executes. Like if we want to change the backgound of something in response to a user clicking on it then we do not want the background to change immideately we want it to change afte the user has clicked on something i.e. in reponse to something, this is where events come in handy.

The follownig are important to look at when learning about events:
- Events - what they are
- Responding to an event - how to listen for an event and respond when one happens
- Event Data - harness the data that is included with an event
- Stopping an event - preventing an event from triggering multiple responses
- Event Lifecycle - the lifecycle stages of an event
- DOM Readiness - events to know when the DOM itself is ready to be interacted with

### monitorEvents()

    monitorEvents(document)
this will monitor all events and show them in the console.
this function is only for chrome.
This takes in two parameter, first is the object on which the everts are to be monitored and second is the type of events to monitor, if the second parameter is not provided then it will monitor all events. For example select and element in the dom and type the following command in the console
    monitorEvents($0, "click")
This will command will execute all the click events in the currently selected dom element.
Once monitoring is started on an element then it will keep monitoring events on it unless it is explicitly unmonitored.
    unmonitorEvents(document)

### getEventListeners()
returns registered events on a specified object.
