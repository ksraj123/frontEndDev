### Reflow & Repaint

**Reflow** is the process of the browser laying out the page. It happens when you first display the DOM (generally after the DOM and CSS have been loaded), and happens again every time something could change the layout. This is a fairly expensive (slow) process.

**Repaint** happens after reflow as the browser draws the new layout to the screen. This is fairly quick, but you still want to limit how often it happens.

For example, if you add a CSS class to an element, the browser often recalculates the layout of the entire page—that's one reflow and one repaint!

Why did adding a little CSS change cause a reflow? What if adding a class changed the position of the element or caused it to float? The browser won't know for certain (and a complete calculation of the impact of a change could take longer than doing the reflow!)

Everytime the DOM is changed some element is added or removed 

https://medium.com/darrja-%E0%A4%A6%E0%A4%B0%E0%A5%8D%E0%A4%9C%E0%A4%BE/what-the-heck-is-repaint-and-reflow-in-the-browser-b2d0fb980c08

https://www.sitepoint.com/saving-bandwidth-by-using-images-the-smart-way/

https://www.sitepoint.com/10-ways-minimize-reflows-improve-performance/

**Side note** - Lazy loading is super cool... must check it out.. 

Let's take a realistic example. Say you're writing the next great blogging platform, and you want to have a "remove spam" button for the administrator. Your HTML looks like this:

    <div id="comments">
        <div class="comment"> <!-- some content --> </div>
        <div class="comment"> <!-- some content --> </div>
        <div class="comment"> <!-- some content --> </div>
    </div>

When we run the spam filter, we discover comments one and two have to be removed.

If we simply call .removeChild() for each of the two comments that need to be removed, that's one reflow and one repaint for each change (so a total of 2 reflows and 2 repaints). We could rebuild the whole thing in a DocumentFragment and replace #comments -- that's the time to rebuild (possibly involving reading files or data), plus at least one reflow and one repaint. 

Or we could hide #comments, delete the spam, and show it again -- that's surprisingly fast, to the cost of one reflow and two repaints (and little else). It's fast because hiding doesn't change the layout, it just erases that section of the screen (1 repaint). When you make the changed section visible again, that's a reflow and a repaint.

    // hide #comments
    document.getElementById("comments").style.display = "none";

    // delete spam comments

    // show #comments
    document.getElementById("comments").style.display = "block";

In general, if you have to make a group of changes, hide/change all/show is a great pattern to use if the changes are relatively contained.

### Virtual DOM

By the way, this is why React and other "virtual DOM" libraries are so popular. You don't make changes to the DOM, but make changes to another structure (a "virtual DOM") and the library calculates the best way to update the screen to match. The catch is you then have to rework your code to use whatever library you're adopting, and sometimes you can do a better job updating the screen yourself (because you understand your own unique situation)