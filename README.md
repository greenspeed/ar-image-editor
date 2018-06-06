# ar-image-editor

Run instruction
Use "yarn serve" to run it locally

A basic image editor
Introduction
One of the areas that Audience Republic takes great pride in is in great design. We spend a lot of money and time on designs and take pride in the way our users interact with our product.

You can see an example of the campaigns that we run for fans here:

https://arep.co/p/the-pleasure-garden-presale-example
Effects
As you've most likely encountered in your front end development work, sometimes patchy browser support means that we've had to implement some effects manually.

One place where we had to to do this was in the background Gaussian blur'ed image in the background of the campaign, which you can see if you look back at the campaign Pleasure Garden.

The blur in the background image is first created by loading the foreground image into a HTML canvas and then blurring it by applying a manual Gaussian blur and setting the background image to the new image. This was done for Safari because at the time it did not support the HTML5 canvas blur property.

Task
I'd like you to do a little experiment with HTML5 canvas.

Take a look at this link:

Image resources

There are 2 files:

brightness-slider-layout.png (1)
pleasure-garden-1200-by-768.png (2)
File (1) shows the layout of a tiny webapp that allows the user too:

Load and display an image file (png or jpg) from the filesystem (using a normal file picker dialog) by clicking on the centre image element,
Once the image has been loaded, the horizontal brightness slider becomes active,
The user can adjust the brightness of the image, in real time, by moving the slider left or right from its centre position to increase brightness by sliding right and decrease brightness by sliding left. NOTE: By "real time" I mean as the slider is dragged, do not wait for a mouse up event to trigger the change in brightness,
EXTRA: If you have time, please add a vertical slider (in the same design as the horizontal slider) that allows the user to adjust the contrast as well (in real time),
Use file (2) as your test file.

What I'll look for:

Attention to detail, it's a very simple web application, so you should be able to design it so it looks exactly like what I've pictured + maybe some additional highlights that fit within the general theme,
Attention to code layout and separation of concerns,
You're creating UI components & following the Atomic design pattern.
You're manipulating the pixel values directly. I realise that HTML5 canvas contains blur and contrast properties, but this exercise is to show that you can also reason about iterating over pixel values and manipulating them appropriately.
Framework
Audience Republic works almost exclusively with Vue.js and we intend to only be using Vue.js in the near future.

As such the solution that you send back should be done within the Vue.js framework.

You can use this project: https://github.com/vuejs/vue-cli to help you start a new Vue.js project and then add too it. If you've not used Vue.js before, the documentation: https://vuejs.org/
