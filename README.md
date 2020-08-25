**The University of Melbourne**
# COMP30019 – Graphics and Interaction

## Workshop 5


# Introduction:

In this lab you will continue learning about shaders, with a particular emphasis on vertex shaders. Vertex shaders are great for manipulating meshes in real-time without needing to regenerate geometry on the CPU (which can be very slow).

You will need to work with three files to start off with:
* **MainScene.unity** – A Unity scene containing a textured plane. This is the scene you’ll be modifying in today’s lab.
* **TileTex.png** – A checkerboard tile image to be used as a texture.
* **TileMaterial.mat** – A Unity material currently using the tile texture.
* **WaveShader.shader** – A Cg/HLSL shader which defines behaviour in parts of the rendering
pipeline. Note that this is not executed on the CPU, but rather the GPU (on a graphics card).

# Task:

1. Open `MainScene.unity` in Unity. You should see a textured plane object on the screen. Currently the ‘Standard’ Unity shader is applied to the plane. Your first task is to assign the shader WaveShader.shader to the plane. This can be done without any code. Recall that shaders are part of an object’s material.

<p align="center">
  <img src="Gifs/1-Cube.png" width="500">
</p>

2. Open `WaveShader.shader`. Open it and examine the vertex shader. Take note of the displacement vector. What effect does it have?

* Modify the vector so that the plane is displaced -5 units in the y-axis (‘up’).

* Modify the vector so that the plane moves upwards. A built-in uniform variable named `_Time.y` should help here. [\*](#Note)

* Modify the vector so that the plane moves up and down in an oscillating fashion. Use the built-in `sin()` function to do this.

<p align="center">
  <img src="Gifs/1-Cube.png" width="500">
</p>

So far everything you have done could have easily been done by setting the object’s transform (i.e. via the MVP matrix). Now you will implement an effect which would be impossible to achieve by simply changing the object’s transform.

3. Use the built-in `sin()` function to displace the y-coordinate of each vertex in terms of its x-coordinate according to the formula `y += sin(x)`. Once this is implemented, you should see a wave effect applied to the plane.

<p align="center">
  <img src="Gifs/1-Cube.png" width="500">
</p>

4. Animate the effect such that waves continuously move through the plane in the x-axis. Use a similar technique to how you animated the plane in question 2.

<p align="center">
  <img src="Gifs/1-Cube.png" width="500">
</p>

5. Modify the effect so that:
* The amplitude of the waves is halved.
* The speed of the waves is doubled.
* The speed of the waves increases with time.

<p align="center">
  <img src="Gifs/1-Cube.png" width="500">
</p>

6. **Challenge** Modify the shader so that the wave effect is occurring in view space rather than model space. This will result in the waves travelling through the object relative to the camera’s orientation. You should verify the effect works by switching to the ‘Scene’ tab and rotating camera around. Hint: Recall that the MVP matrix is a combination of three linear transformations. Presently we displace vertices before applying any of them (they are displaced in model space). You’ll want to change this so that displacement occurs after applying the view matrix. Refer to https://docs.unity3d.com/Manual/SL-UnityShaderVariables.html for some additional variables that could be useful.

<p align="center">
  <img src="Gifs/1-Cube.png" width="500">
</p>

##Note - _Time is a vector whereby the second component contains the number of seconds elapsed since the start of the scene. For reference see: https://docs.unity3d.com/Manual/SL-UnityShaderVariables.html

