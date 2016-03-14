# Changing EasyBox options #

# Inside JavaScript #

Look for `/* custom options here */` inside the `easybox.min.js` file and paste options in JSON format there.

## Example ##

```
{"slideshow": 5000, "loop": true}
```


# Inside HTML #

  1. Create a `<script>` tag with `type="application/json"` and `id="easyOptions"` attributes.
  1. Inside the `<script>` tag, you can write options in JSON.
  1. You can either set options globally by assigning another object to the name `global` containing all options you want to set or you can set options individually for each `rel` attribute by specifying it's value.

## Example ##

Set `loop` loop option for EasyBox globally:

```
<script type="application/json" id="easyOptions">
{
	"global": {
		"loop": true
	}
}
</script>
```

Set `slideshow` option for a specific set:

```
<script type="application/json" id="easyOptions">
{
	"set1": {
		"slideshow": 5000
	}
}
</script>
```

**NOTE:** Everything inside `<div id="easyOptions">` must be valid JSON. Otherwise, EasyBox will not launch!

# Supported options #

## Appearance ##

  * `hideBottom`:
  * `hideCaption`:
  * `hideButtons`:
  * `overlayOpacity`:
  * `resizeDuration`:
  * `resizeEasing`:
  * `fadeDuration`:
  * `captionFadeDuration`:
  * `counterText`:

## Content ##

  * `initCenterSize`:
  * `errorSize`:
  * `defaultContentSize`:
  * `maximumContentSize`:

== Behavior

  * `loop
  * `preloadNext`:
  * `dragDrop`:
  * `noNavigation`:
  * `noClose`:
  * `slideshow`:
  * `autoClose`:

## Keyboard ##

  * `closeKeys`:
  * `previousKeys`:
  * `nextKeys`:
  * `preventOtherKeys`: