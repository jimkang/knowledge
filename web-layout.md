Web layout
====

Safari
---

On Safari, if the svg element comes before a div with `position: fixed`, the div is covered up by the svg.

http://jsbin.com/zoloqup/edit?html,css,output

However, if the div comes first, it stays on top, thereby providing a workable way to have an always-on-top element:

http://jsbin.com/tesurun/2/edit?html,css,output

On Chrome and Firefox, the order in which the svg and div appear in html does not matter.
