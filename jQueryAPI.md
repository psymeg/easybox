

EasyBox works as a jQuery plugin.

# Launching EasyBox from JavaScript #

Call the `$.easybox()` function to launch EasyBox:

```
$.easybox(resources [, startIndex [, options]]);
```

  * `resources`: Array containing resource objects. A resource object has a `url`, `caption`, and optionally `width` and `height` attribute.
  * `startIndex`: Zero-based index specifying the resource shown first.
  * `options`: JavaScript object containing key-value-pairs ([Supported options](ChangeOptions#Supported_options.md))

## Examples ##

```
$.easybox([{url: "/link/to/image.png", caption: "Test image"}]);
```

```
$.easybox([{url: "/link/to/image1.png"},
           {url: "/link/to/image2.png"},
           {url: "/link/to/image3.png"}],
          0, {loop: true});
```

```
$.easybox([{url: "iframe.html", width: 240, height: 120}]);
```

# Close EasyBox #

You can check wheather EasyBox is open via `$.easybox.isOpen()` and close it with `$.easybox.close()`.

## Example ##

```
if ($.easybox.isOpen())
    $.easybox.close();
```

# Enable HTML DOM elements to launch EasyBox when clicked #

The `.easybox` method is an way of enabling EasyBox for DOM elements.

```
.easybox([options [, linkMapper [, linkFilter [, dynamicOptions]]]])
```

  * `options`: JavaScript object containing key-value-pairs ([Supported options](ChangeOptions#Supported_options.md))
  * `linkMapper`: A function taking a DOMElement and returning a resource object from a DOM element.
  * `linkFilter`: A function taking a DOMElement and returning true if an element belongs to the same group. Compare to `this` which is the DOMElement which was initially clicked on.
  * `dynamicOptions`: A function returning a JavaScript object containing key-value-pairs. Remember, that this function should produce the same result for every link in a group.

## Example ##

```
var linkMapper = function(el) {
    // create a resource object with href as url and title as caption
    return {url: el.href, caption: el.title};
};
var linkFilter = function(el) {
    // must return true if the same, otherwise only true if data-group equals
    return (this == el) || ((this.hasAttribute("data-group")) && (this.getAttribute("data-group") == el.getAttribute("data-group")));
};
var dynamicOptions = function(el) {
    // disable drag and drop if specified
    if (el.hasAttribute("data-no-dragdrop"))
        return {dragDrop: false}
    return {}
};
$("a.easybox").easybox({}, linkMapper, linkFilter, dynamicOptions);
```

## The autoload code block ##

The **autoload code block** is the readable code block located by default inside the `easybox.min.js` file of the official EasyBox distribution. This code is using the EasyBox jQuery API to register EasyBox for a specific kind of links, so that it will open when the user clicks on any of these links. The registration is performed as soon as the DOM is ready.

The default implementation registers EasyBox for all links (`<a>` tags) having a `class="lightbox"` attribute.

# Resource Handlers #

In EasyBox v1.3 and above, a resource handler has to be defined for every resource you want to display (image, video, iframe).

You can add a resource handler by calling `$.easybox.resourceHandler`.

```
$.easybox.resourceHandler(handler)
```

  * `handler`: A resource handler object

## The resource handler object explained ##

A resource handler object has the following properties:

  * `identify`: A function taking a resource object and returning true if this handler identifies the resource and is able to load it and create a DOM element to be displayed. This function is called for every resource handler when a resource hasn't been loaded yet.
  * `preLoad`: A function taking a resource object and another function to be called when done pre-loading the resource e.g. via AJAX. This function is called immediately after this handler's `identify` function has returned true.
  * `abort`: A function taking a resource object. This function is called when EasyBox is closing, but the resource hasn't been loaded.
  * `postLoad`: A function taking a resource object and generating a DOM element. This function is called after the `preLoad` function has called loaded() and the resource dimensions have been confirmed.
  * `show`: A function taking a resource object. This function is called immediately after the element has been placed into the container.
  * `hide`: A function taking a resource object. This function is called right before the container is emptied.

### Example 1 ###

```
{
	// identify function
	identify: function(r) {
		// we must have an url
		if (!r.url) return false;
		// return true if it's an image url
		return /(\.jpg|\.jpeg|\.png|\.gif)$/i.test(r.url);
	},

	// preload the image via an Image JavaScript object
	preLoad: function(r, loaded) {
		// create a new image object
		var obj = new Image();
		// called when loaded
		obj.onload = function() {
			// set dimensions of resource object
			r.width = r.width || this.width;
			r.height = r.height || this.height;

			// then call loaded function
			loaded();
		};
		obj.onerror = function() {
			// set error
			r.error = true;

			// always call loaded function
			loaded();
		}

		// pass url to image object
		obj.src = r.url;
	},

	// create DOM object
	postLoad: function(r) {
		r.obj = $("<img src=\""+r.url+"\" width=\""+r.width+"\" height=\""+r.height+"\" alt=\""+r.caption+"\" />")[0];
	}
}
```

### Example 2 ###

This is the default resource handler for displaying inline content:

```
{
	// returns true if an anchor (e.g. #id)
	identify: function(r) {
		if (!r.url) return false;
		var res = /^(.*)\#([A-Za-z0-9\-_]*)$/i.exec(r.url);
		if ((res != null) && ($('#'+res[2]).length)) {
			r.id = res[2];
			return true;
		}
		return false;
	},

	// preloading
	preLoad: function(r, loaded) {
		// get object
		var o = $('#'+r.id)[0];
		if (o) {
			// get dimensions
			r.width = r.width || $(o).width();
			r.height = r.height || $(o).height();
			r.obj = o;
		} else {
			r.error = true;
		}
		loaded();
	},

	// after preloading, conserve original state
	postLoad: function(r) {
		r.parent = $(r.obj).parent()[0];
		r.display = $(r.obj).css('display');
	},

	// after the inline element has been taken from its place and
	// put into the container, show it
	show: function(r) {
		$(r.obj).css('display', 'block');
	},

	// recover original state
	hide: function(r) {
		$(r.parent).append($(r.obj).css('display', r.display));
	}
}
```