Image Loader Util
===================

ImageLoaderWithRescaleSlideShow is a javascript image loading utility. target a div with a width and height, then the array of images can be automatically cropped, centered and animated with CSS3

Usage 
-------------------

Requires Jquery

	<!-- jquery library (required) -->
	<script type="text/javascript" src="js/libs/jquery/jquery-min.js"></script>

Optional libraries, that enhance the animation

	<!-- CSS3 enhances jquery animations (helps with mobile device performance. not necessary) -->
	<script type="text/javascript" src="js/libs/jquery/jquery.animate-enhanced.min.js"></script>

	<!-- Easing Equations by Robert Penner (easeInQuad etc. not necessary) -->
	<script type="text/javascript" src="js/libs/jquery/jquery.easing.js"></script>

Add the image loading library after the other libraries

	<!-- image loading library -->
	<script type="text/javascript" src="js/libs/paulcasey_utils/ImgLoaderWithRescaleSlideShow.js"></script>


Initialise
------------------------

Function 
`Paulcasey.Utils.ImageLoaderWithRescaleSlideShow(etc);`

Arguments
1. theTargetElement: which you would like the image to appear inside (element must have a width and height defined)
2. theImageArray: this can vary from 1 image to dozens
3. theIntervalSpeed: the gap between slides (in milliseconds)
4. theFadeSpeed: the speed that the images fade in (in milliseconds)
5. theRescale: "rescaleEnabled" will resize the image according to the theTargetElement
6. theCentre: "centreEnabled" will center the image inside the theTargetElement
7. theElementResizeListener: "elementResizeListenerEnabled" will bind a listener on theTargetElement, to detect if it resizes, then the image will re-position accordingly. 


Javascript

	$(document).ready(function(){ 
    
	    // multiple images slideshow. listens whether the target element is re-sized, then re-positions accordingly
	    var _il = new Paulcasey.Utils.ImageLoaderWithRescaleSlideShow("#image_target_1", ["images/sample1.jpg", "images/sample2.jpg"], 2000, 1000, "rescaleEnabled", "centreEnabled", "elementResizeListenerEnabled");

	    // single image, no slideshow
	    var _il2 = new Paulcasey.Utils.ImageLoaderWithRescaleSlideShow("#image_target_2", ["images/sample3.jpg"], 1000, 1000, "rescaleEnabled", "centreEnabled", "elementResizeListenerEnabled");

	    // single image, does not listen whether the target element is re-sized so there is less processing taking place
	    var _il3 = new Paulcasey.Utils.ImageLoaderWithRescaleSlideShow("#image_target_3", ["images/sample1.jpg"], 1000, 1000, "rescaleEnabled", "centreEnabled", "elementResizeListenerDisabled");


	});


HTML


	<div id="image_target_1">   
	</div>


	<div id="image_target_2">    
	</div>


	<div id="image_target_3">    
	</div>

CSS


	#image_target_1 {
		margin: 30px;
		width: 200px;
		height: 200px;
		border: solid 1px #333333;
		background-color: #00ff00;
	}
	#image_target_2 {
		margin: 30px;
		width: 300px;
		height: 200px;
		border: solid 1px #333333;
		background-color: #00ff00;
	}
	#image_target_3 {
		margin: 30px;
		width: 60px;
		height: 100px;
		border: solid 1px #333333;
		background-color: #00ff00;
	}


Recommendation: define theElementResizeListener as "elementResizeListenerDisabled" unless you expect theTargetElement to change dimensions. "elementResizeListenerEnabled" will accumulate processing   

