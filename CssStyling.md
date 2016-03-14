# DOM Elements created by EasyBox #

For better understanding, these are the Elements EasyBox creates:

```
<div id="easyOverlay" />
<div id="easyCenter">
	<div id="easyContainer" />
	<div id="easyLoadingIndicator" />
	<div id="easyBottom">
		<div id="easyNavigation">
			<a id="easyPrevLink" href="#" />
			<a id="easyNextLink" href="#" />
		</div>
		<a id="easyCloseLink" href="#" />
		<a id="easySlideLink" href="#" />
		<div id="easyCaption" />
		<div id="easyNumber" />
	</div>
</div>
```

# Template #

You can use this template to create your own styles for EasyBox:

```
/* DON'T CHANGE THIS */
#easyOverlay, #easyCenter, #easyBottom, #easyContainer, #easyLoadingIndicator, #easyNavigation, #easyCaption, #easyNumber, #easyPrevLink, #easyNextLink, #easySlideLink, #easyCloseLink { margin: 0; padding: 0; border: 0 }
#easyOverlay { position: fixed; z-index: 9998;left: 0; top: 0; width: 100%; height: 100%; cursor: pointer }
#easyCenter { position: fixed; left: 50%; top: 50%; z-index: 9999; overflow: hidden }
#easyLoadingIndicator { position: relative; left: 50%; top: 50% }
#easyContainer { overflow: hidden }
#easyContainer img, #easyContainer iframe { border: 0 }
#easyCloseLink, #easySlideLink, #easyPrevLink, #easyNextLink { display: block; outline: none }
#easyCloseLink, #easySlideLink { float: right }
#easyNavigation, #easyPrevLink { float: left }
#easyCaption, #easyNumber { display: block }

/****************************************************************/

#easyOverlay {
	/* overlay background */
	background: #000;
}
#easyCenter {
	/* center background */
	background: #fff;
}
#easyLoadingIndicator {
	/* loading indicator dimensions */
	width: 24px;
	height: 24px;
	/* centered */
	margin-left: -12px; /* -width/2 */
	margin-top: -12px;  /* -height/2 */
	background: url(loading.gif) no-repeat;
}
#easyContainer.error {
	/* error picture */
	background: url(error.png) no-repeat center;
}
#easyContainer {
	padding: 10px;
}

#easyBottom {
	padding: 0 10px 10px 10px;
	font-family: Verdana, Arial, Geneva, Helvetica, sans-serif;
	color: #666;
	text-align: left;
	min-height: 20px;
}

#easyCloseLink {
	width: 20px;
	height: 20px;
	background: transparent url(closebtn.png) no-repeat center;
	margin: 0 0 0 10px;
}
#easySlideLink {
	width: 20px;
	height: 20px;
	background: transparent url(slidebtn.png) no-repeat center;
	margin: 0 0 0 10px;
}
#easySlideLink.disabled {
	background: transparent url(noslidebtn.png) no-repeat center;
}
#easyNavigation {
	float: left;
	width: 38px;
	height: 20px;
	margin: 0 10px 0 0;
}
#easyCaption.nav, #easyNumber.nav {
	/* caption and number moved right by #easyNavigation.width+marginRight when navigation is present */
	margin-left: 48px;
}
#easyPrevLink {
	width: 18px;
	height: 20px;
	background: transparent url(prevbtn.png) no-repeat center;
}
#easyNextLink {
	margin: 0 0 0 20px;
	width: 18px;
	height: 20px;
	background: transparent url(nextbtn.png) no-repeat center;
}
#easyPrevLink.disabled, #easyNextLink.disabled {
	visibility: hidden;
}
#easyCaption, #easyNumber {
	margin-right: 60px;
}
#easyCaption {
	font-size: 12px;
	font-weight: bold;
	line-height: 16px;
	padding-top: 2px;
}
#easyNumber {
	font-size: 10px;
	line-height: 10px;
	height: 10px;
	padding: 4px 0 6px;
}
```