[Home Page](https://github.com/TrackerLounge/Home)

# Tracking And Photogrammetry
Using Photogrammetry to convert a track or footprint into a digital model for further processing

# Introduction
We have a track in our [tracking pit](https://github.com/TrackerLounge/ThreeBoxTrackingPitForTheHomeShop) that we want to convert to a digital model.
<img src='/files/CIMG2574.JPG' width=800>

<img src='/files/trackAsDigitalModel.JPG' width=800>

# Steps to complete
To do this we will:
- Use an ordinary point and shoot camera (e.g. mine is an older Casio Exilim 12.1 Mega-pixel) to take ~30-40 pictures of the track from all angles.
- Use Meshroom (if you have a graphics card that supports CUDA) or Regard3D (if you don't have a graphics card). Both are free software to convert jpg images into a digital mesh model using photogrammetry techniques.
- Use Blender3d to cleanup the mesh (e.g. remove random artifacts), fill any holes, and perform post-processing or analysis.

# Prepping for the Photoshoot
In order for the Meshroom or REgard3D to work and preforem the photogrammetry we need to attend to lighting and markers.

Ensure the track is well light with no shadows (e.g. from you, your camera, or other sources).
I have a very simple setup. I have a LED shoplight taped to a 2x4, resting on two saw horses.
<img src='/files/CIMG2576.JPG' width=800>

Sand, as I have learned from [Experiments with Image Processing, Computer Vision, and Machine Learning and Tracking](https://github.com/TrackerLounge/TrackingAndComputerVision), is noisy. Image processing algorithems really want hard edges to work with in lots of cases. Sand doesn't offer those hard edges. Photogrammetry does better if it can find unique objects in the scene that have hard edges and can be seen at many different scales (e.g. if you scale the image from 4000x3000 pixels, to 400x300 pixels, can you still see those unique objects with unique edges?)

It is a good idea to assume that your images will be scaled (made smaller) at some point in the image processing pipeline.
It is very common for image processing pipelines to create a smaller copy of the original file and then try to do as much work as possible on that smaller image rather than the original image. Depending on the scaling, the reduction in number of pixels processed can be very large. For example, if my original images are 4000x3000 pixels, there are a total of 12,000,000 pixels per image. If That image is scaled to 400x300 pixels, there are a total of 120,000 pixels per image. I typically use about 40 images per track in the photogrammetry process. Unscaled, we have 480,000,000 pixels to process. Scaled, we have just 4,800,000 pixels. The difference in processing time between full and scaled images can be huge - measured in hours. 
<img src='/files/scaledImage.jpg' width=800>

The danger of scaling is that you can lose track of fine details. Tracks are all about very fine details that are easily lost during scaling. 

To help provide the image with hard edges while scaling, I place some cardboard cuttings from a Ziploc box in the scene. Thes have a unique color that makes them easy to tell from the background. They are large enough to be visible if the images are scaled down in pixel size. They produce clean edges if I run an edge-detection algorithm (e.g. Canny Edge Detection, Sobel, Laplace, Differance of Guassian, etc.)

<img src='/files/CIMG2579.JPG' width=800>

The Photogrammetry process is processor expensive. It can take a long time. Sometimes it takes just 12 minutes. In other cases I have seen it run for 23 hours. (A graphics card and powerful processor can speed up the process). It may produce a good model or it may produce garbage. 
Before running photogrammetry on a bunch of images, I like to scale the image in Gimp and apply edge detection to see what a sample image looks like. This helps me avoid wasting time trying to process files that are doome to produce garbage. If I cannot see hard edges in a scaled image, neither will an image processing algorithm.
Here is an example of a scaled imaged that has edge detection run on it. Notice that we have solid edges to work with.
<img src='/files/scaledAndEdgeDetected.JPG' width=400>

I don't know if Meshroom or Regard3D use image scaling or edge-detection but I suspect they do and the photogrammetry seems to work much better/faster when I prepare the track in this way. Note: the edges of the sand container also help with this but are not always distiguishable from all angles.

# Youtube Video of process
[![Alt text](https://github.com/TrackerLounge/TrackingAndPhotogrammetry/blob/master/files/slashScreen.JPG)](https://www.youtube.com/watch?v=6clAcxvFLSM)

If you are interested in how real world scale relates to the scale of the 3D model see
[![Alt text](https://github.com/TrackerLounge/TrackingAndPhotogrammetry/blob/master/files/compareTrackAndModelScaleSplash.jpg)](https://www.youtube.com/watch?v=G0rRLvM_xIw)


For the same process in carpeting see
[![Alt text](https://github.com/TrackerLounge/TrackingAndPhotogrammetry/blob/master/files/WillItTrackPhotogrammetryOnCarpet.jpg)](https://www.youtube.com/watch?v=HMa4Q8ld7XI)

# Blender File
If you would like to take a look at the mesh in blender, the track.blend file can be downloaded from:
<a id="raw-url" href="https://raw.githubusercontent.com/TrackerLounge/TrackingAndPhotogrammetry/master/files/track.zip">Download FILE - track.zip</a>
[track.zip Compressed Blender File](files/track.zip)
Note: the file is pretty big - 35 MB. Github wouldn't let me upload it uncompressed. I zip compressed the track.blend to track.zip. In compressed form it is 14 MB, still big but not too big for Github.

Additional files:
Track in carpeting

<a id="raw-url" href="https://raw.githubusercontent.com/TrackerLounge/TrackingAndPhotogrammetry/master/files/trackOnCarpet_lite.zip">Download FILE - trackOnCarpet_lite.zip</a>

# Research conducted with track digital models
See [Experiments with Image Processing, Computer Vision, and Machine Learning and Tracking](https://github.com/TrackerLounge/TrackingAndComputerVision)

# Additional Resources
I learned how to use Meshroom and Regard3D for Photogrammetry from a number of excellent Youtube videos.
For example, check out: [How to 3D Photoscan Easy and Free!](https://www.youtube.com/watch?v=k4NTf0hMjtY)
