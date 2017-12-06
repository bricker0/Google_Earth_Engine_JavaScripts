# Google_Earth_Engine_JavaScript
This is more of a note to self. I notice that to check my work, I reuse some of the same scripts, and here they are.

## Tips for getting started with GEE
Google Earth Engine (GEE) has lots of tutorials that are easy to follow, easy to modify, and easy to get going! I noticed that when I am putting pieces together, or testing bits of code, there are a few tasks I need to do repeatedly. 1. See if my script renders what I think it should in the map pane 2. Looking up what data and data values are available 3. Exporting imagery 4. Finding single images

# 1. See if my script renders what I want

In the simple example below - I am calling an image to render, it is calling it by it's id and then telling it to render in the map box. Notice, you are not adding any sort of style at all. Just load the data.


Below, you will see that I named the variable elevation because it is calling a dataset related to elevationenter the following script into the script pane in GEE: 

```
// Instantiate an image with the Image constructor to call. 

var elevation = ee.Image('USGS/NED');

//this next line is the one you reuse all the time - render the variable you made in the map window
Map.addLayer(elevation);


```

# 2. Look up what data and data values are available in the data I am calling
You can print information about the data you are working with into the console pane by adding the following to your script

```
print('elevation', elevation);
```
remember to change the variable to whatever you named your variable. Click on console and information about the one elevation band will be revealed.

# 3. export imagery
If you simply say print the image, it will print you an ungly grey sateillite image, you have to be very specific about what you want to export. In this example, notice I am setting the projection, I am setting the pallet, only loading one band, and strechting it. 

```

// Load a single landsat image 
var landsat = ee.Image('LANDSAT/LC8_L1T_TOA/LC82330512015268LGN00')
  
// Create a geometry representing an export region. Barbados - but this isn't called so don't really need it
var geometry = ee.Geometry.Rectangle([-59.6455, 13.0504, -59.4134, 13.3319]);

// Center on Barbados - but this isn't called so don't really need it again
Map.setCenter(-59.5548, 13.1527, 13); // Barbados

//construct a variable I am visualizing Band 1 which is Coastal - Aerosol	0.43-0.45
var visualization = landsat.visualize({
  bands: ['B1'],
  palette: ['green', 'yellow', 'red'],
  max: .4
});

// This will export the image to my drive, the file name will be yellow.
Export.image.toDrive({
  image: visualization,
  description: 'yellow',
  scale: 30
});
```
The output looks like this...not very pretty...but hopefully this helps anyway. 

# 4. Finding single images
I am sure there is an easier way, but I like using <a href="http://snapsat.org/">SnapSat</a> when I am dealing with anything LandSat8 related. With this tool you can easily look up individual file names, path and row of an area. I know you can set intersections to find these using GEE, but I just really like this tool. 

