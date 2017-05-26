# HQ GIF

This technique generates a new color palette to create the gif.
[http://blog.pkh.me/p/21-high-quality-gif-with-ffmpeg.html](http://blog.pkh.me/p/21-high-quality-gif-with-ffmpeg.html)
[https://superuser.com/questions/556029/how-do-i-convert-a-video-to-gif-using-ffmpeg-with-reasonable-quality](https://superuser.com/questions/556029/how-do-i-convert-a-video-to-gif-using-ffmpeg-with-reasonable-quality)

Create a script

	#!/bin/sh

	palette="/tmp/palette.png"

	filters="fps=24,scale=320:-1:flags=lanczos"

	ffmpeg -v warning -i $1 -vf "$filters,palettegen" -y $palette
	ffmpeg -v warning -i $1 -i $palette -lavfi "$filters [x]; [x][1:v] paletteuse" -y $2

Run that script passing in the og file and the desired output
	
	bin/run og.mp4 new.gif