

# Can EasyBox display videos, iFrames and other content? #

Yes, EasyBox can display YouTube and Vimeo videos as well as iFrames and inline elements. Our [Getting started guide](GettingStarted.md) will show you exactly how to do this.

# Can EasyBox automatically resize my images when they are too large to be contained in the browser window? #

Yes, EasyBox automatically shrinks content that is too larte. However, you should resize images before uploading them to save bandwidth.

# EasyBox display is incorrect on my website (sometimes only in a particular browser). What's wrong? #

Most of the time, this is an issue with the CSS of your web page. Check that your CSS rules are valid and do not override EasyBox' CSS rules. In particular, check that there is no margin applied to your `<body>` tag, and that you don't override the default appearance of all `<div>` tags.

If your CSS is correct, you may have invalid or malformed HTML code. Don't expect EasyBox to work well in web pages containing two `<body>` elements, for example.

# Can I change the EasyBox images, colors, fonts, margins, border sizes? #

Yes of course, you just need to edit the values in the `easybox.css` CSS file. It is strongly recommended to minify the CSS file after edit.

EasyBox uses CSS instead of javascript whenever possible.

# EasyBox does not display images containing parenthesis in their URL. What's wrong? #

Parenthesis are invalid characters for URLs. You must use their URL-encoded equivalent instead.

Just replace `(` with `%28` and `)` with `%29`.
You must also replace spaces with `%20` or `+`. Other invalid characters include commas, square brackets, exclamation marks, question marks, semicolons, quotes.

If you're using PHP, the [urlencode() function](http://www.php.net/urlencode) will automatically replace all invalid characters with their URL-encoded equivalent.

# EasyBox does not launch! What can I do? #

First, check if all JavaScript files are embedded correctly. Our [Getting started guide](GettingStarted.md) will show you exactly how to do this.

Second, if you are setting options via `<div id="easyOptions">`, make sure that there is only valid JSON inside the `<div>` tag.

# Is there a way for the visitors of my website to save the images displayed by EasyBox? #

Yes, unlike Slimbox, you can right-click the image and save it.

# Can EasyBox embed Flash content? #

No, not directly. But you can put your Flash contents in an inline element and link to that. Also, you can set a fallback page embedding the flash object for browsers with JavaScript disabled.

  1. Include !SWFObject in your document:
```
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
```
  1. Create an inline container and configure EasyBox to open it when clicked:
```
<a href="myfallback.html#myflash" title="Flash content here" class="lightbox">Click here</a>
<div id="myflash" style="display:none;width:320px;height:240px">
 <p><strong>Your browser does not support Adobe Flash.</strong></p>
</div>
```
  1. Embed your flash object dynamically with SWFObject:
```
<script type="text/javascript">
 swfobject.embedSWF("myflash.swf", "myflash", "320", "240", "9.0.0");
</script>
```