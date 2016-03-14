

# Introduction #

This guide shows you exactly how to install EasyBox and how to use it.

# Installation #

  1. Download a copy of the newest version of EasyBox [here](http://easybox.googlecode.com/files/easybox-v1.4.zip). Alternatively, you can clone the EasyBox git repository:
```
git clone http://easybox.googlecode.com/git easybox
```
  1. Upload the directory `easybox` to your webserver root.
  1. Include jQuery inside the document you want EasyBox to launch in if you haven't already:
```
<script type="text/javascript" src="//ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.min.js"></script>
```
  1. Include the EasyBox JavaScript file inside of your document header:
```
<!-- concatenated -->
<script type="text/javascript" src="/easybox/distrib.min.js"></script>

<!-- seperate files -->
<script type="text/javascript" src="/easybox/easybox.min.js"></script>
<script type="text/javascript" src="/easybox/handlers.min.js"></script>
<script type="text/javascript" src="/easybox/extras/autoload.min.js"></script>
```
  1. Include the EasyBox CSS file inside of your document header:
```
<link rel="stylesheet" href="/easybox/styles/default/easybox.min.css" type="text/css" media="screen" />
```

You're now ready to use EasyBox.

# Usage #

## Single image ##

To show an image with EasyBox, you have to create a link pointing to the image file with an additional `lightbox` class. You can also specify a `title` attribute. This will be shown below the image.

Paste the following code inside the `<body>` tag of your document to show an image with EasyBox:

```
<a href="/link/to/image.jpg" title="Image caption" class="lightbox">Image title</a>
```

## YouTube/Vimeo video ##

It's basically the same as [displaying an image](GettingStarted#Single_image.md), except that you link to the YouTube or Vimeo video.

```
<a href="http://www.youtube.com/watch?v=VIDEO_ID" title="Video caption" class="lightbox">Video title</a>
```

EasyBox will automatically determine the aspect ratio of the YouTube video or the video dimensions of the Vimeo video before displaying it. If you want, you can specify the height of the video by either setting the `ytPlayerHeight` option or by using the `data-height` attribute:

```
<a href="http://www.youtube.com/watch?v=VIDEO_ID" title="Video caption" class="lightbox" data-height="480">Video title</a>
```

## iFrame ##

Same here, you just link to the page you want to display in an iFrame inside EasyBox:

```
<a href="http://www.example.com" title="Example page" class="lightbox">Example page</a>
```

If you want to set iFrame width and height, you have to specify `data-width` and `data-height`.

```
<a href="http://www.example.com" title="Example page" class="lightbox" data-width="320" data-height="240">Example page</a>
```

## Inline element ##

  1. Append a `<div>` tag to the bottom of the `<body>` tag and give it a unique `id` attribute.
  1. Set the CSS property `display: none`.
  1. Specify width and height. EasyBox will need this values later.
  1. Create a link pointing to `#unique_id`.

```
<a href="#unique_id" title="Inline element" class="lightbox">Click here</a>
<div id="unique_id" style="display:none;width:320px;height:240px">
 <p>Some content here...</p>
 <p>More content...</p>
</div>
```

You can even specify a URL to a page in case EasyBox is not compatible with the visitor's browser or JavaScript is disabled.

```
<a href="/path/to/fallback.php#unique_id" title="Inline element" class="lightbox">Click here</a>
<div id="unique_id" style="display:none;width:320px;height:240px">
 <p>Some content here...</p>
 <p>More content...</p>
</div>
```

## Display sets ##

You can also display collections of all supported elements inside EasyBox and navigate through them with previous/next links.

Specify a unique set name by passing a `data-group` attribute.

```
<a href="/link/to/image1.jpg" title="Image caption" class="lightbox" data-group="set">Image title</a>
<a href="/link/to/image2.jpg" title="Image caption" class="lightbox" data-group="set">Image title</a>
<a href="/link/to/image3.jpg" title="Image caption" class="lightbox" data-group="set">Image title</a>
```

This will also work with videos, iFrames and inline elements.

## Slideshows ##

You can make every set a slideshow by setting the `slideshow` option to a value specifying the number of milliseconds an element is shown.

```
<script type="application/json" id="easyOptions">
{
	"set1": {
		"slideshow": 5000
	}
}
</script>
<a href="/link/to/image1.jpg" title="Image caption" class="lightbox" data-group="set1">Image title</a>
<a href="/link/to/image2.jpg" title="Image caption" class="lightbox" data-group="set1">Image title</a>
<a href="/link/to/image3.jpg" title="Image caption" class="lightbox" data-group="set1">Image title</a>
```

## Presentation ##

With EasyBox, you can create a presentation that automatically slides and closes. Therefore, you have to call the `$.easybox()` API function.

```
<script type="text/javascript">
(function($) {
	$(function() {
		$("#presentation").click(function() {
			$.easybox([{url: '#slide1', caption: "Slide 1"}, {url: '#slide2', caption: "Slide 2"}, {url: '#slide3', caption: "Slide 3"}], 0, {
				slideshow: 5000,    // automatically slide forward
				autoClose: 5000,    // automatically close at the end
				hideBottom: true,   // hide bottom container
				noNavigation: true, // disable navigation keys
				noClose: true       // disable close keys
			});
		});
	});
})(jQuery);
</script>
<a id="presentation" href="#">Click here</a>
<div id="slide1" style="display:none;width:320px;height:240px">
 <p>Some content here...</p>
 <p>More content...</p>
</div>
<div id="slide2" style="display:none;width:320px;height:240px">
 <p>Next slide...</p>
</div>
<div id="slide3" style="display:none;width:320px;height:240px">
 <p>Last slide...</p>
</div>
```

# Change EasyBox behavoir #

Learn how to [change EasyBox options](ChangeOptions.md).

# Advanced EasyBox jQuery API #

You can call EasyBox from JavaScript, add resource handlers for displaying unsupported content or change default options.

Just check out the [jQuery API documentation](jQueryAPI.md) to get started.