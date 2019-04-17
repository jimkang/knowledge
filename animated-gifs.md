# Animated Gifs

## Creating animated gifs from a video file

- Resize your video. 
  - `ffmpeg -i complete-graph.mp4 -filter:v scale=500:490 -c:a copy complete-graph-small.mp4` 
  - (Change scale to the actual size you want.)
- Create a palette from your video. (When I went straight to making gif, things got muddy.) 
  - `ffmpeg -i complete-graph-small.mp4 -vf fps=15,scale=500:-1:flags=lanczos,palettegen palette.png`
- Use the palette to create the gif.
  - `ffmpeg -i complete-graph-small.mp4 -i palette.png -filter_complex "fps=15,scale=420:476:flags=lanczos[x];[x][1:v]paletteuse" -ignore_loop 0 complete-graph.gif`
  - [ignore_loop tells ffmpeg to ignore the looping setting from the input video](https://stackoverflow.com/a/25556286/87798). By default, it will loop gifs infinitely, but videos usually say not to loop, so ffmpeg will respect that unless told otherwise. 

## Creating an animated gif from images with ImageMagick

- Resize your images to a reasonable size.
  - e.g. `convert -resize 1024x1024 steak1.jpg steak1.jpg`
  - Or `convert -resize 25% steak1.jpg steak1.jpg`
- Combine them into an animated gif.
  - `convert -loop 0 -delay 100 steak*.jpg grill-rotation.gif`
    - This will put a 1-second delay in between frames. 
