# Cropping video

    ffmpeg -i in.mp4 -filter:v "crop=900:900:540:128" out.mp4

That crops a video to 900x900, starting at an upper left of 540,128. [More here.](https://video.stackexchange.com/a/4571)
    
# Trimming video

    ffmpeg -i pizzas.ogv -ss 00:00:04 -t 00:00:10 -c copy pizzas-cut.ogv

Trims a video, starting at four seconds, then keeps the next ten seconds.
