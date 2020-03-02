# Image editing

`convert` and `mogrify` are from ImageMagick.

## Append images to an image, in vertical orientation

     convert +append guys.png source-images/*.png guys.png
 
## Resize all images in a directory to a max dimension

     mogrify -resize 128x128\> -path source-images/resized source-images/*.png
     
## Place all images in a directory into square canvasses, in-place

     mogrify -gravity center -background transparent -extent 128x128 source-images/resized/*.png
