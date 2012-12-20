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
	<script type="text/javascript" src="js/libs/cosmos/cosmos-image-loader.1.01.js"></script>


Initialise
------------------------

Function 
`Cosmos.Utils.ImageLoaderWithRescaleSlideShow(etc);`

Arguments
1. theTargetElement: which you would like the image to appear inside (element must have a width and height defined)
2. theImageArray: this can vary from 1 image to dozens
3. theIntervalSpeed: the gap between slides (in milliseconds)
4. theFadeSpeed: the speed that the images fade in (in milliseconds)
5. theRescale: "rescaleEnabled" will resize and crop the image according to the theTargetElement. "rescaleInnerEnabled" will resize the so it does not crop inside theTargetElement
6. theCentre: "centreEnabled" will center the image inside the theTargetElement. "topAlignEnabled" will align the image to the top of theTargetElement
7. theElementResizeListener: "elementResizeListenerEnabled" will bind a listener on theTargetElement, to detect if it resizes, then the image will re-position accordingly. 


Javascript

	$(document).ready(function(){ 
    
	    // multiple images slideshow. listens whether the target element is re-sized, then re-positions accordingly, with success and error callbacks
	    var _il = new Cosmos.Utils.ImageLoaderWithRescaleSlideShow("#image_target_1", ["images/sample1.jpg", "images/sample2.jpg"], 2000, 1000, "rescaleEnabled", "centreEnabled", "elementResizeListenerEnabled", {success:customImageLoadedHandler, error:customImageLoadErrorHandler});

	    // single image, no slideshow
	    var _il2 = new Cosmos.Utils.ImageLoaderWithRescaleSlideShow("#image_target_2", ["images/sample3.jpg"], 1000, 1000, "rescaleEnabled", "centreEnabled", "elementResizeListenerEnabled");

	    // single image, does not listen whether the target element is re-sized so there is less processing taking place
	    var _il3 = new Cosmos.Utils.ImageLoaderWithRescaleSlideShow("#image_target_3", ["images/sample1.jpg"], 1000, 1000, "rescaleEnabled", "centreEnabled", "elementResizeListenerDisabled");

	    // single image, resizes to fit the entire image inside the div (instead of cropping)
	    var _il4 = new Cosmos.Utils.ImageLoaderWithRescaleSlideShow("#image_target_4", ["images/sample1.jpg"], 1000, 1000, "rescaleInnerEnabled", "centreEnabled", "elementResizeListenerDisabled");

	    // single image, aligns to the top of the target element (instead of the centre)
	    var _il5 = new Cosmos.Utils.ImageLoaderWithRescaleSlideShow("#image_target_5", ["images/sample1.jpg"], 1000, 1000, "rescaleInnerEnabled", "topAlignEnabled", "elementResizeListenerDisabled");


	});


HTML


	<div id="image_target_1">   
	</div>


	<div id="image_target_2">    
	</div>


	<div id="image_target_3">    
	</div>


	<div id="image_target_4">    
	</div>


	<div id="image_target_5">    
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
	#image_target_4 {
		margin: 30px;
		width: 60px;
		height: 100px;
		border: solid 1px #333333;
		background-color: #00ff00;
	}
	#image_target_5 {
		margin: 30px;
		width: 60px;
		height: 100px;
		border: solid 1px #333333;
		background-color: #00ff00;
	}


Optional listeners
---------------------
You can add success and error callbacks detect when the images are all loaded in the element

`var _il = new Cosmos.Utils.ImageLoaderWithRescaleSlideShow("#image_target_1", ["images/sample1.jpg", "images/sample2.jpg"], 2000, 1000, "rescaleEnabled", "centreEnabled", "elementResizeListenerEnabled", {success:customImageLoadedHandler, error:customImageLoadErrorHandler, change:customImageChangeHandler});`

When the images are loaded, this calls the following function (which was defined in the constructor) 

	// OPTIONAL: LISTENS WHEN LOADED
    function customImageLoadedHandler(e){
      // IMAGES ARE LOADED
      console.log("SUCCESS: The images are now loaded on element: " + e.data("theTargetElement") + ". The images are: "+e.data("theImageArray"));
    }


When an image does not load, this calls the following function (which was defined in the constructor) 

    // OPTIONAL: LISTENS WHEN NOT LOADED   
    function customImageLoadErrorHandler(e){
      console.log("ERROR: One of the following images could not load: "+e.data("theImageArray"));
    }

When an image slide changes, this calls the following function (which was defined in the constructor) 

    // OPTIONAL: LISTENS WHEN THE SLIDESHOW IMAGE CHANGES  
    function customImageChangeHandler(e){
      console.log("CHANGE: you are now viewing: "+e.data("curImageSrc")+" (id: "+e.data("curImageId")+"), on the element: "+ e.data("theTargetElement"));
    }


Performance recommendation
---------------------
Please define theElementResizeListener as "elementResizeListenerDisabled" unless you expect theTargetElement to change dimensions. "elementResizeListenerEnabled" will accumulate processing   

