# Cropping video

    ffmpeg -i in.mp4 -filter:v "crop=900:900:540:128" out.mp4

That crops a video to 900x900, starting at an upper left of 540,128. [More here.](https://video.stackexchange.com/a/4571)
    
