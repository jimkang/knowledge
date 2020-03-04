# Image editing

`montage` and `mogrify` are from ImageMagick.

## Append images to an image, in vertical orientation (single column of images)

     montage $(RESIZEDDIR)/*.png -tile 1x -background Transparent -geometry '1x1+0+0<' static/sheet.png
 
 You can do `x1` to create a row of images instead. The `-geometry '1x1+0+0<'` [tells it to not resize and to not add padding](https://www.imagemagick.org/Usage/montage/#zero_geometry). And (I think) it tells it to retain the aspect ratio.
 
## Resize all images in a directory to a max dimension

     mogrify -resize 128x128\> -path source-images/resized source-images/*.png
     
## Place all images in a directory into square canvasses, in-place

     mogrify -gravity center -background transparent -extent 128x128 source-images/resized/*.png
