Description
==================
A CSS scale transition/animation can lead to blurry images.

Besides, when combined with a transform-origin or translate, it can be tricky to precisely anticipate what the result of a scale transformation.

This class provides a light and precise zoom/dezoom animation with constant image sharpness. The zoom and dezoom areas can be defined with precision with a tool like Photoshop.

[Demo](https://projects.thibautfoussard.com/git/zoomer/example/).



Usage
==================

Zoom/dezoom areas
------------------
First, use an image tool like Photoshop to define where the animation should start and end, on a given image.


![zoomer_areas](https://projects.thibautfoussard.com/git/zoomer/zoomer_areas.jpg)


Then, retrieve the width, height, x and y of the start area (here in red). They will later be used as JS parameters.


![zoomer_areas_2](https://projects.thibautfoussard.com/git/zoomer/zoomer_areas_2.jpg)


Then do the same for the next step (in green).


Code
------------------

An `<img>` tag allows the JS class to start its initialization on the `load` event.
However, the actual rendering will only take place in the canvas, hence the `opacity: 0` applied on the `img` tag.


```html
<img id="image" src="image.jpg" style="opacity: 0">
<canvas id="canvas"></canvas>
```

Instanciate by passing the dimensions and coordinates of the previously defined steps.
At least 2 steps must be defined (a start and an end), but you can add as many as needed. 

```javascript
var zoom = new Zoom({
    format   : {width: 300, height: 250},
    canvas   : "canvas",
    img      : "image",
    steps    : [
        {width: 300, height: 250, x: 74, y: 30}, // start
        {width: 448, height: 373, x: 0,  y: 0, duration: 3000}, // next step
        // add as many steps as needed
    ],
    easing   : function() { } // Optional. easeInOutQuad by default.
});
	
zoomer.start();
```


Easing
==================

By default, the Zoomer uses an easeInOutQuad easing.
However, others equations can be used. See [Robert Penners equations](https://forum.kirupa.com/t/robert-penners-easing-equations-in-pure-js-no-jquery/330985).