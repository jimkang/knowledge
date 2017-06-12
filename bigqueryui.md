BigQuery UI
----

- The element that contains the result rows (that get removed and added as the window resizes) is a `table` with the attribute `ng-if="rtCtrl.displaySlowContent"` and the class `records-table`.
- Table redrawing can be triggered by dragging the divider between the query and result views. It will trigger a MouseEvent listener on a `div` with the id `query-dragger`. If the mouse button is lifted away from the dragger, there is also a listener on `document`.
  - The `MouseEvent` is the first param passed to it. It has a `type` of `mousedown`, `mousemove`, or `mouseup` and `screenX`, `screenY`, `clientX`, and `clientY` coordinates. Row adding/deleting seem to happen as a result of all three types.
  - How does it decide what to add?
  var queryDragger = document.getElementById('query-dragger');
  queryDragger.dispatchEvent(new MouseEvent('mousedown', {screenX: 500, screenY: 2000, clientX: 500, clientY: 1900}))
