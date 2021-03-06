```
cacheable: false
```

[Starter files](/~tmullen/secure/f17cg/cs315-hw6.zip)

## Exercise 1: Projection Matrix

In this exercise, you'll work with a simulation of perspective projection. Your task will be to set the values of the `projectionMatrix` variable such that the simulation behaves as shown in this video:

<video width="480" height="360" controls>
  <source src="/~tmullen/images/cg/perspectiveProj.ogv" type="video/ogg;" codecs="theora, vorbis">
Your browser does not support the video tag.
</video>

The way the simulation works is as follows. The "3D scene" consists of 12 colored circles positioned around the space between the front and back of the view volume (frustum), represented in transparent gray. These are collected in a single Three.js `Object3D` object called `threeDScene`. The "projection" consists of creating a copy of this object and transforming it using the `projectionMatrix` matrix such that it is projected onto the image plane space. The resulting projection should depend on the shape of the frustum generated by moving the image plane nearer or farther from the center of projection (`cop`) with the focal length slider. Note that the apparent size of the circles in the projection differs by distance, and that some circles only appear in the projection when the angle of the frustum is sufficiently wide. The "Curtain" slider enables you to view the projection on its own, without seeing the original unprojected 3D scene, in order to make it clearer what's going on. The "Clip image plane" check box enables you to turn on and off clipping the projected scene to the image plane dimensions.

There's a lot of starter code in this exercise, but your task involves a very small amount of actual code. Review how homogeneous coordinates are used to represent perspective projection in a matrix and read the code and comments to know which values in the code you'll need to use to derive the correct values for the matrix. 

### Readme question

**Answer the following question(s) in your readme:** Once you have the perspective projection matrix working properly, try checking the "Keep projections" checkbox in the GUI. This leaves each projected scene object in the Three.js scene, so you can see how they look side by side. Uncheck the "Clip image plane" check box and slide the focal length back and forth a few times to get a stack of projections in the scene. What do these stacks of projected circles tell you about this transformation? Specifically, would you be able to tell by looking at them whether or not perspective projection is a linear transformation? Explain your answer. 

## Exercise 2: Camera setup in Three.js

In this exercise you're going to get a little practice working with the camera. This exercise relates to what you read in the second part of Chapter 2 of *Learning Three.js*, "Different cameras for different uses". You will need to understand how the perspective camera works and what its properties represent. You'll also put your trigonometry skills to use again to animate the camera moving in a circle.

When you run the HTML code for this exercise in a browser, you should see something like this:  

![Starter Image](/~tmullen/images/cg/elephant_start.png)

Clearly, there are few problems. The first one you'll notice is that portions of the scene are getting cut off and aren't being rendered at all. Rotate the scene around with your mouse a bit and see if you can get a sense of what's being excluded from rendering and why.

### Objective

Your assignment is to modify the settings of the camera and then to animate the position of the camera so that your scene displays as shown in this video (your scene's camera should rotate continuously):

<video width="480" height="360" controls>
  <source src="/~tmullen/images/cg/elephant.ogv" type="video/ogg;" codecs="theora, vorbis">
Your browser does not support the video tag.
</video>

### Perspective camera settings

The first thing you need to do is to get the camera settings right. Review the description of the perspective camera's behavior in *Learning Three.js* Chapter 2.

As you adjust the camera's settings, you'll see also that the camera's position is important to how the scene displays. When the field of view is wider, things will seem further away because they occupy less of the image. You will need to eyeball it a bit to get the camera's distance from the target and its field of view set to values that look like the solution video above. Note that the perspective effects are clear in the grid and the plane under the elephant. Grid squares that are further from the viewer appear considerably smaller than ones that are close to the viewer.

### Animating the camera

Most of the animation code will be inside the `render()` function. Since the movement of the camera is around the `y` axis, the `y` value won't need to change, while the others do. Loop through degrees in a circle and use the `Math.cos()` and `Math.sin()` functions to position your camera on each call of the `render()` function. Remember that the `render()` function runs in the `animate()` loop, so you won't have any need for a `for` loop. Also, don't forget that the JS trig functions want radians for arguments, so you'll need to convert the degrees of your angles to radians.


## Exercise 3: Lighting in Three.js

In this exercise you'll get some practice setting up lights. Specifically, you'll add some colored spotlights to a scene and animate their position and direction using GUI sliders. You should have read Chapter 3 in *Learning Three.js* to be sure you understand the differences between light types and the specifics of the `THREE.SpotLight` object. This assignment will also give you a hands-on introduction to how colored light mixes.  

Begin by downloading the [starter file](/~tmullen/cg/f16/cs315-hw6.zip). When you run the HTML code in a browser, you should see something like this:  

![Starter Image](/~tmullen/images/cg/elephantLightStart.png)

You can rotate the scene with your mouse. As you can see, the elephant is lit by a single white spot light. Read the code for the specifics of how the spot light is set up, and make sure you understand what the various parameters are doing.

### Objective

Your assignment is to modify the scene such that rather than being lit by a single white spot light, the elephant is lit by three colored spotlights: red, green, and blue. The three spotlights' positions should be controlled by a slider with the label `lightSeparation`. When the slider value is 0, the three lights are positioned together, resulting in the appearance of a white light (red, green, and blue light combine to make white). When the slider value goes to one, the three colors separate, illuminating the elephant from the left, right, and front in three different colors, as shown in the video here:

<video width="480" height="360" controls>
  <source src="/~tmullen/images/cg/elephantLights.ogv" type="video/ogg;" codecs="theora, vorbis">
Your browser does not support the video tag.
</video>

In addition, you should also set up the spot lights' target objects, and have the targets controllable with a separate slider. This controls where the spot lights point. As you can see in the video, when the slider is at its maximum, the spot lights are directed over the top of the elephant, when it is at its minimum, they are directed at the zero point of the 3D space.


### Setting up spot lights and targets

The first thing you need to do is to set up the lights appropriately. You should make your own decisions about the positioning of the lights to get an effect as close to the video above as you can. The current position of the white spot light should be a good guide for getting started. The three colored lights will be added to the scene in a very similar way to the white spotlight in the starter (you don't want a white light in the final scene, so you will either get rid of or alter the initial white spot light).

Every spot light has an attribute called `target` which represents an actual 3D object toward which the spot light points. To use this object, it must be added to the scene. Read the comments in the starter file for more on this.

### Animating the lights

Once again, the main part of the animation code will occur within the `render` function. The `gui` object has already been set up for you, along with one of the controls, `lightSeparation` in the `controls` object. You'll need to add the second control `target`. Both controls should range from 0.0 to 1.0 and act as factors for whatever displacement you choose for your target or light positions.


### Extra challenge

Try to do something comparable with area light objects. AreaLights are not standard in Three.js, but they are discussed in Chapter 3 of "Learning Three.js". Read the instructions for using area lights and set up a scene that uses them in place of spotlights. You won't get identical effects, but experiment with what can and can't be done with area lights. For extra credit, turn in the area light project in addition to the main assignment project.

## Submitting

Upload the project to its own directory inside your `public_html` directory using FileZilla. Be sure that all dependencies are in place and **Double check that your finished work displays properly in a browser online.** 

In Moodle, submit **only** the link to your assignment directory on the shared server containing the fully implemented assignment and readme.txt.
The Moodle page for this assignment is [here](https://moodle.pugetsound.edu/moodle/mod/assign/view.php?id=407322).
