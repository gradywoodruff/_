# FFMPEG

###Show between second 0 and 20

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