![](assets/images/tumblr.gif)

# Tumblr Themeing
Custom Tumblr theme from scratch

The first thing I do is create the structure of the website in my text editor. I try to do 100% of the coding and editing within the text editor and constantly check it by selecting the whole page, copying, going to the browser, pasting in the entire code and checking it in the Tumblr preview. This way I can have readable code and keep a repository.

### Reminders
* Only upload theme assets in the "Theme Assets" section
* External images or assets can be blocked by Tumblr. Upload all assets to Tumblr (external font links can be added to the header though)
* Sometimes you have to re-generate an asset link

### Documentation
* [Tumblr Docs](https://www.tumblr.com/docs/en/custom_themes)

### Get Started
1. Click the name of your blog at the top of the Dashboard or under the list icon at the top.
2. Click “Customize” on the right column.
3. Click “Edit HTML” below the theme thumbnail on the left.

### General Structure
Start custom theme with this markup

	<html>
	    <head>
	        <title>{Title}</title>
	        <link rel="shortcut icon" href="{Favicon}">
	        <link rel="alternate" type="application/rss+xml" href="{RSS}">
	        {block:Description}
	            <meta name="description" content="{MetaDescription}" />
	        {/block:Description}
	    </head>
	    <body>
	        <h1>{Title}</h1>

	        {block:Description}
	            <p id="description">{Description}</p>
	        {/block:Description}

	        <ol id="posts">
	            {block:Posts}{block:Text}
	                    <li class="post text">
	                        {block:Title}
	                            <h3><a href="{Permalink}">{Title}</a></h3>
	                        {/block:Title}{Body}
	                    </li>
	                {/block:Text}{block:Photo}
	                    <li class="post photo">
	                        <img src="{PhotoURL-500}" alt="{PhotoAlt}"/>

	                        {block:Caption}
	                            <div class="caption">{Caption}</div>
	                        {/block:Caption}
	                    </li>
	                {/block:Photo}{block:Panorama}
	                    <li class="post panorama">
	                        {LinkOpenTag}
	                            <img src="{PhotoURL-Panorama}" alt="{PhotoAlt}"/>
	                        {LinkCloseTag}{block:Caption}
	                            <div class="caption">{Caption}</div>
	                        {/block:Caption}
	                    </li>
	                {/block:Panorama}{block:Photoset}
	                    <li class="post photoset">
	                        {Photoset-500}{block:Caption}
	                            <div class="caption">{Caption}</div>
	                        {/block:Caption}
	                    </li>
	                {/block:Photoset}{block:Quote}
	                    <li class="post quote">
	                        "{Quote}"

	                        {block:Source}
	                            <div class="source">{Source}</div>
	                        {/block:Source}
	                    </li>
	                {/block:Quote}{block:Link}
	                    <li class="post link">
	                        <a href="{URL}" class="link" {Target}>{Name}</a>

	                        {block:Description}
	                            <div class="description">{Description}</div>
	                        {/block:Description}
	                    </li>
	                {/block:Link}{block:Chat}
	                    <li class="post chat">
	                        {block:Title}
	                            <h3><a href="{Permalink}">{Title}</a></h3>
	                        {/block:Title}

	                        <ul class="chat">
	                            {block:Lines}
	                                <li class="{Alt} user_{UserNumber}">
	                                    {block:Label}
	                                        <span class="label">{Label}</span>
	                                    {/block:Label}{Line}
	                                </li>
	                            {/block:Lines}
	                        </ul>
	                    </li>
	                {/block:Chat}{block:Video}
	                    <li class="post video">
	                        {Video-500}{block:Caption}
	                            <div class="caption">{Caption}</div>
	                        {/block:Caption}
	                    </li>
	                {/block:Video}{block:Audio}
	                    <li class="post audio">
	                        {AudioEmbed}{block:Caption}
	                            <div class="caption">{Caption}</div>
	                        {/block:Caption}
	                    </li>
	                {/block:Audio}{/block:Posts}
	        </ol>

	        <p id="footer">
	            {block:PreviousPage}
	                <a href="{PreviousPage}">&#171; Previous</a>
	            {/block:PreviousPage}{block:NextPage}
	                <a href="{NextPage}">Next &#187;</a>
	            {/block:NextPage}

	            <a href="/archive">Archive</a>
	        </p>
	    </body>
	</html>

### Tricks
You can use the blocks for css classes and ids. For instance, below is an example of a body tag where I added:
* `{block:TagPage}{/block:TagPage}` to insert a body id only on Tag pages
* `body-{URLSafeTag}` to give the id a specific tag id that can be customized for each different tag in CSS
* `{block:PermalinkPage}{/block:PermalinkPage}` to insert a body class only on permalink pages

	<body data-spy="scroll" data-target="#drops-spy" {block:TagPage} id="body-{URLSafeTag}" class="tag_page" {/block:TagPage}{block:PermalinkPage} class="perma_page" {/block:PermalinkPage}{block:SearchPage} class="search_page" {/block:SearchPage}>

### Custom Pages
To generate custom pages:
1. "Add a page"
2. "Custom Layout"
3. Do not turn on "Show a link to this page"
4. Enter a custom url path
5. Paste code.

The preview on these custom pages has never worked for me. You have to edit blindly and open up the site in another window to check

### Advanced Options
* Turn off "Use default mobile theme"
* Turn off "Promote Tumblr!" if you don't want the buttons in the top right and the popup in the bottom right
* Custom CSS is found in the Advanced Options. I also keep this in a seperate file and if I have any changes, I copy and paste the entire css file in each time to make sure I'm always keeping my text file updated with my Tumblr code