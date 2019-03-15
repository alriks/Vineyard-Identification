# Vineyard-Identification
A project to identify and mark vineyards. Globally.

How many vineyards are there in the world? Where are they? What is the climate 
and weather like in those locations? How are changes in the weather and eventually 
the climate going to change the production and quality of wine in the world?

It's a seemingly simple question that gets very complicated quickly.

There were about 6.7 million ha of vines in production globally in 2017. There are 
1.5 billion ha of agricultural production globally. So vineyard production is only 
.004 percent of global agriculture.

If you want to know where wine is growing in the world, you're going to have to go 
out and find it hidden within a hystack of agricultural production.

Fortunately, most viticulture occurs in relatively restricted geographic areas. 
The global limitations are pretty basic.

<i>Vitis vinifera</i> grows globally between 30 and 50 degrees North and South 
latitiude. These areas are roughly contiguous with temperature bands between 
10 and 20C

<hr>
<img src= ./images/30-50.jpg>
<hr>

This still leaves a lot of ground to cover. Satellite imagery is an obvious starting 
point. A quick examination of several options leads to the realization that the level
of detail needed will be quite high:
<img src=./images/scales.png>

<i>These are images of the same area in Napa Valley California at differing 
resolutions: Landsat, 30m, Sentinel 2a, 10m, Planet Labs, ~3m, and the National 
Agricultural Imagery Program, ~1m per pixel.</i>

In the Landsat scene, you can pick out towns and agricultural areas. Sentinel gives 
you a better sense of the boundaries. The Planet imagery allows you to pick out individual 
fields, but not to know what crops are growing in them. At the NAIP imagery's resolution, 
you can see the specific detail that marks the grapes laid out in rows and blocks.

The next sensible step would be to outline the actual grape fields themselves so that you 
could have a better sense of the boundaries of the fields. Google's Earth Engine does an
admirable job of this, but you have to essentially hand draw the boundaries in order for 
them to accurately reflect field edges:

<img src=./images/yountville_ndvi_2018.jpg>

<i>This image shows NDVI values for all of the individual fields in the Yountville AVA 
calculated on July 19, 2018. Imagery from the National Agricultural Imagery Program, 
~1m per pixel.</i>

But if we have the rough perimeters of the regions within which we might look for a
specific pattern and we have plenty of imagery of vineyards from above, that might be 
a perfect case for a deep learning network. Picking out repeated patterns from more 
imagery than you might have time to look at yourself is a perfect job for a computer.

So I started using a library from Fastai to look at imagery of California with the hope 
of outlining all of the vineyard fields in the AVAs in the state at 1m/pixel scale.

The workflow is:
1. gather training data for the model
2. train up a deep learning network and measure the accuracy of its output
3. teach it to recognize vineyards within aerial imagery
4. outline and label the individual fields

For the training data to be useful it has to show both the vineyards we're interested
in and other types of landscape features that might show up in the imagery we will be 
using for the testing phase. I downloaded two images for final testing, one of the 
Napa Valley around Yountville and one of the area around the village of Mersault in 
Burgundy.

In order to provide training data for these two areas I used a previously built dataset
from the University of California, Merced. The dataset contains 2100 images manually 
extracted from larger images in the USGS National Map Urban Area Imagery collection 
for various urban areas around the country. The pixel resolution of this public domain 
imagery is 1 foot. The dataset can be found <a href="http://weegee.vision.ucmerced.edu/datasets/landuse.html">here</a>.



