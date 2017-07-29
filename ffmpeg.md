# FFMPEG

## Show between second 0 and 20

	ffmpeg -i input.mp4 -i image.png \
	-filter_complex "[0:v][1:v] overlay=25:25:enable='between(t,0,20)'" \
	-pix_fmt yuv420p -c:a copy \
	output.mp4

`overlay=25:25` means we want to position the image 25px to the right and 25px down, originating from the top left corner (0:0).

`enable='between(t,0,20)'` means we want the image to show between second 0 and 20.

`[0:v][1:v]` means that we want the first video file we import with -i, in our case input.mp4 or how ffmpeg sees it video input file number 0, to be under video input file 1, in our case image.png. :v just means we want video 0 and video 1. `[0:a]` would mean we want the first imported audio track. Which would also come from input.mp4 but would point to the audio track instead of the video track in the mp4 file.

If you want a certain image quality/settings and not the settings ffmpeg chooses, add the image and or audio encoding options you want to use. The default video encoder will be x264. Check the H.264 encoding guide for possible settings.

The `-acodec copy` / `-c:a copy` that you have in your command f.e. would simply re-use the audio from the source file. Though you can't do that with the video of course (in this case), that has to be transcoded.

If you want to transcode audio, remove the `-c:a copy` part. You may have to explicitly specify an encoder, e.g. `-c:a aac -strict experimental`. See the AAC encoding guide for more info.


## Fade out

	ffmpeg -i in.mp4 -framerate 30000/1001 -loop 1 -i logo.png -filter_complex
	  "[1:v] fade=out:st=30:d=1:alpha=1 [ov]; [0:v][ov] overlay=10:10 [v]" -map "[v]"
	  -map 0:a -c:v libx264 -c:a copy -shortest out.mp4

This assumes that the logo is a single still image with an alpha channel and you want to overlay it over a video with a frame rate of 30000/1001 (NTSC rate). Change the `-framerate` to match your input video if it is different. If your logo is a video then omit `-framerate 30000/1001 -loop 1`. If the logo does not have an alpha channel, add one by inserting e.g. `format=yuva420p,` immediately before `fade`.

This will display the logo at x,y position 10,10 for 30 seconds followed by a 1 second fade out.

The reason for the `-framerate` and `-loop` for a still image is so that the fade out will work. If there is only a single frame then it has no way to fade out over a 1 second interval. Ideally it should be the same frame rate as the video so that the fade will be as smooth as possible.

## Using overlay video filter to add a logo to a video:

	ffmpeg -i video.mp4 -i logo.png -filter_complex "[0:v][1:v]overlay" \
	-codec:a copy out.mp4

To understand this command you need to know what a [stream specifier](http://ffmpeg.org/ffmpeg.html#Stream-specifiers-1) is and reading the [Introduction to FFmpeg Filtering](http://ffmpeg.org/ffmpeg-filters.html#Filtering-Introduction) will help. `[0:v]` refers to the video stream(s) of first input (`video.mp4`), and `[1:v]` refers to the video stream of the second input (`logo.mp4`). This is how you can tell `overlay` what inputs to use. You can omit [0:v][1:v], and overlay will still work, but it is recommended to be explicit and not rely on possibly unknown defaults.

By default the logo will be placed in the upper left.

Using `-codec:a copy` will [stream copy](http://ffmpeg.org/ffmpeg.html#Stream-copy) the audio. This simply re-muxes the audio instead of re-encoding it. Think of it as a "copy and paste" of the audio.

### Moving the logo

This example will move the logo 10 pixels to the right, and 10 pixels down: enter image description here

	ffmpeg -i video.mp4 -i logo.png -filter_complex "[0:v][1:v]overlay=10:10" \
	-codec:a copy out.mp4

This example will move the logo 10 pixels from the right side and 10 pixels down:


	ffmpeg -i video.mp4 -i logo.png -filter_complex \
	"[0:v][1:v]overlay=main_w-overlay_w-10:10" -codec:a copy out.mp4

`main_w` refers to the width of the "main" input (the background or `[0:v]`), and `overlay_w` refers to the width of the "overlay" input (the logo or `[1:v]`). So, in the example, this can be translated to `overlay=320-90-10:10` or `overlay=220:10`.

### Timing the overlay

Some filters can handle [timeline editing](http://ffmpeg.org/ffmpeg-filters.html#Timeline-editing) which allows you to use [arithmetic expressions](http://ffmpeg.org/ffmpeg-utils.html#Expression-Evaluation) to determine when a filter should be applied. Refer to `ffmpeg -filters` to see which filters support timeline editing.

This example will show the logo until 30 seconds:

	ffmpeg -i video.mp4 -i logo.png -filter_complex \
	"[0:v][1:v]overlay=10:10:enable=between(t\,0\,30)" -codec:a copy out.mp4