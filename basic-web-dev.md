# Basic web development

## Dragging DOM elements

Non-SVG, non-Canvas ones that is.

[Here is an example that works on both mobile and desktop browsers.](https://jsbin.com/fakuma/1/edit?html,js,console,output)

Key points:

- Mouse events do not apply to mobile browsers, at least, as of 2019-10-09. You do actually need to listen to touch events.
- It's a lot less overwhelming to track deltas in mouse/touch position once you're in dragging mode and use that to calculate current position for the draggable element instead of working from the event properties to determine where in the various nested boxes the mouse/touch is and where the draggable is in relation to that.
- window.pageX and window.pageY are nice in that they're not affected by scrolling the way that clientRects are. (e.g. When the user scrolls, `window.pageY - the last window.page Y value` is accurate without having to add any scroll properties as you need to do with clientRects.)
- You want to listen to mouseup/touchend and mousemove/touchmove events globally if you're using them for the purposes of figuring out when a drag ended and where it's going, not on the draggable element itself.
- Style properties come back from the DOM API as strings, with units on them, no less. You need to be careful when doing math with them. And when you set style properties, your values will be quietly rejected if they don't have units.
