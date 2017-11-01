# youtube_dl

### youtube-dl args
All possible args for youtube_dl `ydl_opts`

	username:          Username for authentication purposes.
	password:          Password for authentication purposes.
	videopassword:     Password for acces a video.
	usenetrc:          Use netrc for authentication instead.
	verbose:           Print additional info to stdout.
	quiet:             Do not print messages to stdout.
	no_warnings:       Do not print out anything for warnings.
	forceurl:          Force printing final URL.
	forcetitle:        Force printing title.
	forceid:           Force printing ID.
	forcethumbnail:    Force printing thumbnail URL.
	forcedescription:  Force printing description.
	forcefilename:     Force printing final filename.
	forceduration:     Force printing duration.
	forcejson:         Force printing info_dict as JSON.
	dump_single_json:  Force printing the info_dict of the whole playlist
	                   (or video) as a single JSON line.
	simulate:          Do not download the video files.
	format:            Video format code. See options.py for more information.
	format_limit:      Highest quality format to try.
	outtmpl:           Template for output names.
	restrictfilenames: Do not allow "&" and spaces in file names
	ignoreerrors:      Do not stop on download errors.
	nooverwrites:      Prevent overwriting files.
	playliststart:     Playlist item to start at.
	playlistend:       Playlist item to end at.
	playlistreverse:   Download playlist items in reverse order.
	matchtitle:        Download only matching titles.
	rejecttitle:       Reject downloads for matching titles.
	logger:            Log messages to a logging.Logger instance.
	logtostderr:       Log messages to stderr instead of stdout.
	writedescription:  Write the video description to a .description file
	writeinfojson:     Write the video description to a .info.json file
	writeannotations:  Write the video annotations to a .annotations.xml file
	writethumbnail:    Write the thumbnail image to a file
	writesubtitles:    Write the video subtitles to a file
	writeautomaticsub: Write the automatic subtitles to a file
	allsubtitles:      Downloads all the subtitles of the video
	                   (requires writesubtitles or writeautomaticsub)
	listsubtitles:     Lists all available subtitles for the video
	subtitlesformat:   Subtitle format [srt/sbv/vtt] (default=srt)
	subtitleslangs:    List of languages of the subtitles to download
	keepvideo:         Keep the video file after post-processing
	daterange:         A DateRange object, download only if the upload_date is in the range.
	skip_download:     Skip the actual download of the video file
	cachedir:          Location of the cache files in the filesystem.
	                   False to disable filesystem cache.
	noplaylist:        Download single video instead of a playlist if in doubt.
	age_limit:         An integer representing the user's age in years.
	                   Unsuitable videos for the given age are skipped.
	min_views:         An integer representing the minimum view count the video
	                   must have in order to not be skipped.
	                   Videos without view count information are always
	                   downloaded. None for no limit.
	max_views:         An integer representing the maximum view count.
	                   Videos that are more popular than that are not
	                   downloaded.
	                   Videos without view count information are always
	                   downloaded. None for no limit.
	download_archive:  File name of a file where all downloads are recorded.
	                   Videos already present in the file are not downloaded
	                   again.
	cookiefile:        File name where cookies should be read from and dumped to.
	nocheckcertificate:Do not verify SSL certificates
	prefer_insecure:   Use HTTP instead of HTTPS to retrieve information.
	                   At the moment, this is only supported by YouTube.
	proxy:             URL of the proxy server to use
	socket_timeout:    Time to wait for unresponsive hosts, in seconds
	bidi_workaround:   Work around buggy terminals without bidirectional text
	                   support, using fridibi
	debug_printtraffic:Print out sent and received HTTP traffic
	include_ads:       Download ads as well
	default_search:    Prepend this string if an input url is not valid.
	                   'auto' for elaborate guessing
	encoding:          Use this encoding instead of the system-specified.
	extract_flat:      Do not resolve URLs, return the immediate result.
	                   Pass in 'in_playlist' to only show this behavior for
	                   playlist items.
	postprocessors:    A list of dictionaries, each with an entry
	                   * key:  The name of the postprocessor. See
	                           youtube_dl/postprocessor/__init__.py for a list.
	                   as well as any further keyword arguments for the
	                   postprocessor.
	progress_hooks:    A list of functions that get called on download
	                   progress, with a dictionary with the entries
	                   * filename: The final filename
	                   * status: One of "downloading" and "finished"

	                   The dict may also have some of the following entries:

	                   * downloaded_bytes: Bytes on disk
	                   * total_bytes: Size of the whole file, None if unknown
	                   * tmpfilename: The filename we're currently writing to
	                   * eta: The estimated time in seconds, None if unknown
	                   * speed: The download speed in bytes/second, None if
	                            unknown

	                   Progress hooks are guaranteed to be called at least once
	                   (with status "finished") if the download is successful.


	The following parameters are not used by YoutubeDL itself, they are used by
	the FileDownloader:
	nopart, updatetime, buffersize, ratelimit, min_filesize, max_filesize, test,
	noresizebuffer, retries, continuedl, noprogress, consoletitle

	The following options are used by the post processors:
	prefer_ffmpeg:     If True, use ffmpeg instead of avconv if both are available,
	                   otherwise prefer avconv.
	exec_cmd:          Arbitrary command to run after downloading

### URLs

As of 20171002, the URLs for the thumbnails of YouTube videos are:

	https://img.youtube.com/vi/__youtubecode__/0.jpg
	https://img.youtube.com/vi/__youtubecode__/1.jpg
	https://img.youtube.com/vi/__youtubecode__/2.jpg
	https://img.youtube.com/vi/__youtubecode__/3.jpg
	https://img.youtube.com/vi/__youtubecode__/mqdefault.jpg
	https://img.youtube.com/vi/__youtubecode__/hqdefault.jpg
	https://img.youtube.com/vi/__youtubecode__/maxresdefault.jpg