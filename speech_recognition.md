![](assets/images/hal.gif)

## Open Source Speech Recognition
I followed a few different repositories and some youtube videos to build the beginning of a speech recognition program

### Pocket Sphinx
(from [pocketsphinx-ruby](https://github.com/watsonbox/pocketsphinx-ruby))
>This gem depends on [Pocketsphinx](https://github.com/cmusphinx/pocketsphinx) (libpocketsphinx), and [Sphinxbase](https://github.com/cmusphinx/sphinxbase) (libsphinxbase and libsphinxad). The current stable versions (0.8) are from late 2012 and are now outdated. Build them manually from source, or on OSX the latest development (potentially unstable) versions can be installed using [Homebrew](http://brew.sh/) as follows ([more information here](https://github.com/watsonbox/homebrew-cmu-sphinx)).
> 
>Add the Homebrew tap:
	
	$ brew tap watsonbox/cmu-sphinx

>You'll see some warnings as these formulae conflict with those in the main reponitory, but that's fine.
> 
>Install the libraries:
	
	$ brew install --HEAD watsonbox/cmu-sphinx/cmu-sphinxbase
	$ brew install --HEAD watsonbox/cmu-sphinx/cmu-pocketsphinx

### Install the Updated Shphinx Train 
Download [sphinxtrain-5prealpha.tar.gz](https://sourceforge.net/projects/cmusphinx/files/sphinxtrain/5prealpha/sphinxtrain-5prealpha.tar.gz/download) and unzip in the same directory.

	cd sphinxtrain-5prealpha
	./configure
	make
	make install
	cd ..

### Customize Recognition Settings
(partially followed this [tutorial](https://youtu.be/IAHH6-t9jK0))
Create a new speech folder
	
	cd assets
	mkdir speech
	cd assets/speech

### Download the Enligsh Model
[cmusphinx-en-us-ptm-5.2.tar.gz](https://sourceforge.net/projects/cmusphinx/files/Acoustic%20and%20Language%20Models/US%20English/cmusphinx-en-us-ptm-5.2.tar.gz/download)

Rename this unzipped folder to `en-us-download`



### Testing Files
Next create some test reate test files. I recorded myself reading a poem and split each audio stanza into a seperate numbered `.wav` file, then created plaintext files for File IDs and transcriptions

1. Numbered audio files **RECORDINGS AT SAMPLE RATE OF 16 KHZ (16000) AND IN MONO WITH SINGLE CHANNEL.**
2. A plaintext File IDs file named [audiofile].fileids
3. A transcription file named [audiofile].transcription

The files should look like

	1.wav  
	2.wav
	.....
	12.wav
	audio.fileids
	audio.transcription

[audioname].fileids shoud be formatted like:

	1
	2
	3
	4
	5
	6
	7
	8
	9
	10
	11
	12

[audiofile].transcription should be formatted with `<s></s>` tags surrounding each line and a `(#)` with the corresponding audio file name in the parentheses. **NO CAPITAL LETTERS OR SYMBOLS**:

	<s> there is a place where the sidewalk ends </s> (1)
	<s> and before the street begins </s> (2)
	<s> and there the grass grows soft and white </s> (3)
	<s> and there the sun burns crimson bright </s> (4)
	<s> and there the moon bird rests from his flight </s> (5)
	<s> to cool in the peppermint wind </s> (6)
	<s> let us leave this place where the smoke blows black </s> (7)
	<s> and the dark street winds and bends </s> (8)
	<s> past the pits where the asphalt flowers grow </s> (9)
	<s> we shall walk with a walk that is measured and slow </s> (10)
	<s> and watch where the chalk-white arrows go </s> (11)
	<s> to the place where the sidewalk ends </s> (12)

Then copy more dependencies 
	
	cp -a /usr/local/share/pocketsphinx/model/en-us/cmudict-en-us.dict .
	cp -a /usr/local/share/pocketsphinx/model/en-us/en-us.lm.bin .

Then create `.mfc` files out of each `.wav` file

	sphinx_fe -argfile en-us-download/feat.params -samprate 16000 -c test.fileids -di . -do . -ei wav -eo mfc -mswav yes

Copy over some Sphinx Train files

	cp /usr/local/libexec/sphinxtrain/bw .
	cp /usr/local/libexec/sphinxtrain/map_adapt .
	cp /usr/local/libexec/sphinxtrain/mk_s2sendump .

Then run

	./bw -hmmdir en-us-download -moddeffn en-us-download/mdef -ts2cbfn .ptm. -feat 1s_c_d_dd -svspec 0-12/13-25/26-38 -cmn current -agc none -dictfn cmudict-en-us.dict -ctlfn test.fileids -lsnfn test.transcription -accumdir .

	cp -a en-us-download en-us-jj

	./map_adapt -moddeffn en-us-download/mdef -ts2cbfn .ptm. -meanfn en-us-download/means -varfn en-us-download/variances -mixwfn en-us-download/mixture_weights -tmatfn en-us-download/transition_matrices -accumdir . -mapmeanfn en-us-jj/means -mapvarfn en-us-jj/variances -mapmixwfn en-us-jj/mixture_weights -maptmatfn en-us-jj/transition_matrices

	pocketsphinx_continuous -hmm en-us-jj -lm en-us.lm.bin -dict cmudict-en-us.dict -infile audio.wav > audio.txt

I wrote a Ruby program to automate this process, Readme on that coming soon