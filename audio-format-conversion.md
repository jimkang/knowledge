# Converting several ogg files to mp3

    #!/bin/bash

    root=.

    for file in *.ogg

    do
        basename="${file%.*}"
        opusdec ${file} ${basename}.wav
        lame ${basename}.wav ${basename}.mp3
    done

# Converting several ogg files to wav, concatenating them, then converting the concatenated file to an mp3

    #!/bin/bash

    prefix=whatever

    for file in ${prefix}*.ogg

    do
        basename="${file%.*}"
        opusdec ${file} ${basename}.wav
    done

    # https://superuser.com/a/587512
    ffmpeg -f concat -safe 0 -i <( for f in ${prefix}*.wav; do echo "file '$(pwd)/$f'"; done ) combined.wav

    lame combined.wav ${prefix}-complete.mp3

# Extracting audio from a video

    ffmpeg -i undefined.ogv -vn -acodec copy out.ogg
