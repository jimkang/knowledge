BigQuery UI
----

- The element that contains the result rows (that get removed and added as the window resizes) is a `table` with the attribute `ng-if="rtCtrl.displaySlowContent"` and the class `records-table`.
- Table redrawing can be triggered by dragging the divider between the query and result views. It will trigger a MouseEvent listener on a `div` with the id `query-dragger`. If the mouse button is lifted away from the dragger, there is also a listener on `document`.
  - The `MouseEvent` is the first param passed to it. It has a `type` of `mousedown`, `mousemove`, or `mouseup` and `screenX`, `screenY`, `clientX`, and `clientY` coordinates. Row adding/deleting seem to happen as a result of all three types.
  - How does it decide what to add?
    - There's a variable that has a `last` property in `$digest` that changes. How is that determined?
    - The `MouseEvent` `pageX` and `pageY` are used in a call to some `resize` function.
 ```
  function l(a) {
    c.resize(h.resizeName, a.pageX - n, a.pageY - q);
    e || (d.$applyAsync(f.bind(g, this)),
    e = !0)
  }
  ```
    Where `q` seems to correspond to `clientY`.

```
var x = 500;
var startY = 300;
var endY = 4000;
var startEvent = {screenX: x, screenY: startY, clientX: x, clientY: startY, pageX: x, pageY: startY};
var endEvent = {screenX: x, screenY: endY, clientX: x, clientY: endY, pageX: x, pageY: endY};
var queryDragger = document.getElementById('query-dragger');


function sendMouseMove() {
  queryDragger.dispatchEvent(new MouseEvent('mousemove', endEvent));
  setTimeout(sendMouseUp, 200);
}

function sendMouseUp() {
  queryDragger.dispatchEvent(new MouseEvent('mouseup', endEvent));
}

queryDragger.dispatchEvent(new MouseEvent('mousedown', startEvent)); 
setTimeout(sendMouseMove, 200);
```
