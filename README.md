jazzhands.js
============

Javascript library for simplified LEAP motion gesture binding.  Please note, this library is still in Alpha.  Version 1.0 is planned to retain the existing event bindings, but have a more maintainable code-base.

## Getting started
Clone repository locally 
https://github.com/troygdaniel/jazzhands.git
## Demos
Interactive documentation:
http://troygdaniel.com/jazz/documentation.html#/start

Three.js Lensflare demo:
http://troygdaniel.com/threejs/examples/webgl_lensflares.html

Three.js Orbiting Earth demo:
http://troygdaniel.com/threejs/examples/misc_controls_fly.html

2 minute youtube video demo:
http://youtu.be/kW1VjxEqcCM

## Basic implementation
~~~javascript
// Get ready
Jazz.init();

// Get set
Jazz.on('navigation', function(n) {
    // n is string with one of the following values:
    // "right", "left", "down", "up", "zoomIn", "zoomOut"
    console.log("Go " +n+ "!");
});
~~~

## More options
Additional options allow you to use bind finger events and use your hand for direct manipulation.

### Implementing finger bindings
~~~javascript
// During init setting up the "helper" text for fingers
Jazz.init({
    fingersText: ["Zoom Out?","Zoom in!"]
});

// Alternatively, you can set up the helper text anytime after the init
Jazz.setFingersText(["Zoom Out?","Zoom in?"])

// fingers in this example will either equal 1 or 2
Jazz.on("fingers", function(fingers) {
    console.log("on fingers = " + fingers);
});

// Clearing the finger event bindings
Jazz.clearFingersText();

~~~

### Jazz UI options
~~~javascript
// Change the navigation wait timer
Jazz.WAIT_FINGER_MS=900

// Completely hide the Jazz UI
Jazz.show();

// Show the Jazz UI
Jazz.hide();

// Toggle the display of "helper arrows" by setting  
Jazz.disableHelper = false

// Toggle the display of the navigation timer 
Jazz.disableTimer = false
~~~

### Direct manipulation (Grab, release and progress)
~~~javascript
// Get ready
Jazz.init()

// The user has clenched their fist in anger
Jazz.on("grab", function () {
    console.log("Grabbing");
});

// The user has opened their mind and hand
Jazz.on("release", function (progress) {
    console.log("Release");
});

// The user has moved their hand movements, tilts, pitch and yaw
// The movements are measured in % relative progressions
Jazz.on("progress", function (progress) {
    var upPercent = progress["up"]; // ... down, up, left, right
    var zoomOut = progress["zoomOut"]; // ... zoomIn
    var rollRight = progress["rollRight"]; // ... rollLeft
    var yawRight = progress["yawRight"]; // ... yawLeft
});            

~~~

### Native leapJS event access
~~~javascript
// g = CircleGesture, KeyTapGesture, ScreenTapGesture
Jazz.on("gestures", function (g) { 
    console.log(g.type);
});

// leap JS frames
Jazz.on("frames", function (f) {
    console.log(f.currentFrameRate+","
                +hands.length+","
                +f.fingers.length);
});
~~~
