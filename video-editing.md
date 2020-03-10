# Cropping video

    ffmpeg -i in.mp4 -filter:v "crop=900:900:540:128" out.mp4

That crops a video to 900x900, starting at an upper left of 540,128. [More here.](https://video.stackexchange.com/a/4571)
    
# Trimming video

    ffmpeg -i pizzas.ogv -ss 00:00:04 -t 00:00:10 -c copy pizzas-cut.ogv

Trims a video, starting at four seconds, then keeps the next ten seconds.

# Changing speed

    ffmpeg -i crabbington-0.ogv -filter:v "setpts=0.5*PTS" crabbington-0-double-speed.ogv

# Making animated gifs

[Animated gifs](animated-gifs.md)

# Adding audio from a wav file to a video

    ffmpeg -i cat-chase.mov -i ~/Music/yakety-sax-6s.wav -c:v copy -c:a aac -shortest -map 0:v:0 -map 1:a:0 cat-chase.mp4
  
 `-shortest ` tells it to make the output as long as the shortest of the two inputs. `-map 0:v:0` tells it to use the video from the first input in the first (only output) and `-map 1:a:0` tells it to use the audio from the second (1-indexed) input in the output.
 
