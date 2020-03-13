# Audio

## White noise machine

    play -c1 -r 4k -t s8 /dev/urandom
    
(play comes from `sox`.) Via [Substack](https://www.youtube.com/watch?v=2oz_SwhBixs)

## Stereo silence

sox -n -r 48000 -c 2 Silence_250ms.wav trim 0.0 0.250
