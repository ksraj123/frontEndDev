### Event Phases

There are three different phases during the lifecycle of an event. They are:

- the capturing phase
- the at target phase
- and the bubbling phase

In all modern browsers first the capturing phase runs it comes from top of the document to the clicked elements then it bubbles back up till it reaches to top, it jumps from level to level and does not trigger adjacent elements on the same level, its easier to show it by code.

Lets consider the following html

	<div id="parent">
		<div id="subParent">
			<div id="child1">Child 1</div>
			<div id="child2">Child 2</div>
		</div>
	</div>

now lets consider the following javascript for this html

	parent.addEventListener("click", ()=>{console.log("parent Clicked");});
	subParent.addEventListener("click", ()=>{console.log("subParent Clicked");});
	child1.addEventListener("click", ()=>{console.log("child1 Clicked");});
	child2.addEventListener("click", ()=>{console.log("child2 Clicked");});

when child1 is clicked then the output is - child1 Click  subParent Clicked  prent clicked
when child2 is clicked then the output is - child2 Click  subParent Clicked  prent clicked

this happens so because when click happens then it comes from top to botton in capturing phase then it does not do anything as the third argument for `addEventListener` is to useCapturing or not which is false by default so the work out in the bubbleing phase

when its at its target child1 or child2 then it does not trigger adjacent elements and bubbles up and triggers it parents event listerners listening to the same kind of events

	parent.addEventListener("click", ()=>{console.log("parent Clicked");}, true);
	subParent.addEventListener("click", ()=>{console.log("subParent Clicked");});
	child1.addEventListener("click", ()=>{console.log("child1 Clicked");}, true);
	child2.addEventListener("click", ()=>{console.log("child2 Clicked");});

when child1 is clicked then the output is - prent clicked child1 Clicked subParent Clicked
when child2 is clicked then the output is - prent clicked child2 Clicked subParent Clicked


### Event Objects

When an event occurs, the browser includes an event object. This is just a regular JavaScript object that includes a ton of information about the event itself. This event object is passed to the callback function of the eventLitener it triggers. This object is the object of the type of the event and its attributes can be learned about by looking at the docuemntation for interface of that event type. This event object is also printed by monitorEvents() function of chrome


### The Default Action
One common reason to use the event object is to prevent the default action from happening.

Think about an anchor link on a webpage. There are probably a couple dozen links on this page! What if you wanted to run some code and display some output when you click on one of these links. If you click on the link, it will automatically navigate you to the location listed in its href attribute: that's what it does by default.

What about a form element? When you submit a form, by default, it will send the data to the location in its action attribute. What if we wanted to validate the data before sending it, though?

Without the event object, we're stuck with the default actions. However, the event object has a .preventDefault() method on it that a handler can call to prevent the default action from occurring!

    const links = document.querySelectorAll('a');
    const thirdLink = links[2];

    thirdLink.addEventListener('click', function (event) {
        event.preventDefault();
        console.log("Look, ma! We didn't navigate to a new page!");
    });