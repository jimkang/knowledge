Canvas
===

- [The `arc` instruction is different from the `arcTo` instruction in SVG.](https://www.kirupa.com/html5/drawing_circles_canvas.htm)
  - The first two params are the center of the circle it's going around.
  - The third is the radius.
  - The fourth and fifth are the starting and ending *angles* of the arc, in radians.
  - The sixth is a flag that means go counterclockwise if true, clockwise otherwise.
  - Here's how you draw a circle with it:
 
        ctx.beginPath();
        ctx.moveTo(starPoint.x, starPoint.y - starRadius);
        ctx.arc(
          starPoint.x, starPoint.y,
          starRadius,
          0,
          2 * Math.PI,
          false
        );
        ctx.fill();
  
