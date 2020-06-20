[Home Page](https://github.com/TrackerLounge/Home)

# Tracking And Photogrammetry
Using Photogrammetry to convert a track or footprint into a digital model for further processing

# Introduction
We have a track in our [tracking pit](https://github.com/TrackerLounge/ThreeBoxTrackingPitForTheHomeShop) that we want to convert to a digital model.
<img src='/files/CIMG2574.JPG' width=800>

# Steps to complete
To do this we will:
- Use an ordinary point and shoot camera (e.g. mine is an older Casio Exilim 12.1 Mega-pixel) to take ~30-40 pictures of the track from all angles.
- Use Meshroom (if you have a graphics card that supports CUDA) or Regard3D (if you don't have a graphics card). Both are free software to convert jpg images into a digital mesh model using photogrammetry techniques.
- Use Blender3d to cleanup the mesh, fill any holes, and preform post-processing or analysis.

# Prepping for the Photoshoot
In order for the Meshroom or REgard3D to work and preforem the photogrammetry we need to attend to lighting and markers.

Ensure the track is well light with no shadows (e.g. from you, your camera, or other sources).
I have a very simple setup. I have a LED shoplight taped to a 2x4, resting on two saw horses.
<img src='/files/CIMG2576.JPG' width=800>

Sand, as I have learned from [Experiments with Image Processing, Computer Vision, and Machine Learning and Tracking](https://github.com/TrackerLounge/TrackingAndComputerVision), is noisy. Image processing algorithems really want hard edges to work with in lots of cases. Sand doesn't offer those hard edges. Photogrammetry does better if it can find unique objects in the scene that have hard edges and can be seen at many different scales (e.g. if you scale the image from 4000x3000 pixels, to 400x300 pixels, can you still see those unique objects with unique edges?)

To help provide the image with hard edges, I place some cardboard cuttings from a Ziploc box in the scene. Thes have a unique color that makes them easy to tell from the background. They are large enough to be visible if the images are scaled down in pixel size. They produce clean edges if I run an edge-detection algorithm (e.g. Canny Edge Detection, Sobel, Laplace, Differance of Guassian, etc.)

<img src='/files/CIMG2579.JPG' width=800>

<img src='/files/scaledAndEdgeDetected.JPG' width=400>

I don't know if Meshroom or Regard3D use image scaling or edge-detection but I suspect they do and the photogrammetry seems to work much better/faster when I prepare the track in this way. Note: the edges of the sand container also help with this but are not always distiguishable from all angles.

# Additional Resources
I learned how to use Meshroom and Regard3D for Photogrammetry from a number of excellent Youtube videos.
For example, check out: [How to 3D Photoscan Easy and Free!](https://www.youtube.com/watch?v=k4NTf0hMjtY)
