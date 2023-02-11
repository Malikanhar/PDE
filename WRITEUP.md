# Fish / Shrimp Pond Detection and Area Estimation

## Goals
- To estimate fish/shrimp pond area from a latitude and longitude coordinate
- To get geo-location information of the fish/shrimp pond

## Solution
The first thing that I do is to explore the possible solution to achieve the goals. Since the only information that I have is the `latitude` and `longitude` coordinate of the pond, so this problem could be solved by utilizing satellite image. There are several satellite imagery providers:
- [Google Earth](http://earth.google.com)
- [Sentinel Hub](https://www.sentinel-hub.com)
- [World Imagery Wayback](https://livingatlas.arcgis.com/wayback)
- [Zoom Earth](https://zoom.earth)

From all providers above, I decided to use the [Google Earth Engine](https://earthengine.google.com) since it has more support for the developer in order to process the satellite imagery, it also has an online compiler and you can access this project from the following url https://code.earthengine.google.com/7d1c912aee08df38f715085f3a9880ad.

Here's what I got by visualizing one of the shrimp pond location.

<center><img src="https://github.com/Malikanhar/PDE/raw/main/assets/landsat_8.PNG" width="600"></center>

Then, I'm reading some articles to filter the water surface from the satellite imagery. There's a method called NDWI (Normalized Difference Water Index) that uses Shortwave infrared-1 and Near Infrared bands of sensing images. The NDWI can enhance water information efficiently in most cases. It is sensitive to build-up land and result in over-estimated water bodies. And here's what I got by applying NDWI formula to my code.

<center><img src="https://github.com/Malikanhar/PDE/raw/main/assets/ndwi.PNG" width="600"></center>

As we can see that using NDWI we can localize the water surface, but it's not clear enough, since there are a lot of noise (non water surface classified as a water body). So that, this formula is modified by changing the use of Near Infrared to Green band, this new formula known as MDWI (Modified Normalized Difference Water Index). And here's what I got by applying MNDWI formula.

<center><img src="https://github.com/Malikanhar/PDE/raw/main/assets/mndwi.PNG" width="600"></center>

Now, the water surface are more clear than before, and we can easily localize the shrimp pond location. The next thing that I do is applying canny edge detector so that I can find the pond contours.

<center><img src="https://github.com/Malikanhar/PDE/raw/main/assets/canny.PNG" width="600"></center>

Since the poor quality of satellite imagery, it's quite difficult for me to apply the contours detection on that. But in summary, we can localize the fish/shrimp pond by using the satellite imagery, and it would be good if we have an access to the high quality of satellite sensing image.

In addition to get the geo-location infromation of the fish/shrimp pond coordinate, I have created a [notebook](https://colab.research.google.com/drive/1MeeJKWbb1Coa76mPMC36D0pbFeTA4sSD?usp=sharing) to accomplish that task.