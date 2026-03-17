---
layout: post
title: "Make webcomics easily"
date: 2012-09-30
original_url: "https://thebayesianobserver.wordpress.com/2012/09/30/make-webcomics-easily/"
categories: ["creativity", "productivity"]
---
I have wanted to draw webcomics for at least the last 3 years, but never got around to figuring out an easy way to do it. Drawing on a computer with a mouse is a disaster. There are special tablets like [Wacom](http://www.wacom.com/)‘s that artists use (I believe [xkcd](http://xkcd.com/) uses Wacom’s tablet). There are also some high-end, expensive iPad apps (e.g. [brushes](http://www.brushesapp.com/)). But I wanted to do very simple drawing and without spending any money. I finally decided to put together a easy to use method for drawing simple black & white comics.

I think the simplest way to draw a webcomic is low-tech:

1. Draw on paper with a black marker.
2. Take a picture with your phone and upload to a computer. Unfortunately, a picture taken by a phone is not simple b&w, but contains many colours, graininess of the paper, the effect of lighting, etc. Therefore:
3. Run the picture though a pixel thresholder.

I wrote a small python program to threshold the value of each pixel and make each pixel either pure white or pure black. The result allows me to go from the JPG picture on the left (taken with an iPhone 3GS) to the PNG image on the right:

[![](/images/make-webcomics-easily-img-1.png "Screen shot 2012-09-29 at 9.08.16 PM")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/09/screen-shot-2012-09-29-at-9-08-16-pm.png)

Each pixel in the left image is simply an integer between 0 and 255 (after converting to grayscale). Now, this should be easy to do using a basic image editing program by ‘converting to B&W’, but the caveat is that one cannot simply use a threshold of 128 because the pixels corresponding to blank space on the paper may not necessarily be below 128. The result of using a fixed threshold of 128 was a disaster:

[![](/images/make-webcomics-easily-img-2.png "Screen shot 2012-09-29 at 9.21.36 PM")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/09/screen-shot-2012-09-29-at-9-21-36-pm.png)

There is probably a menu option somewhere on a good image editor to do what I want, but I don’t want to deal with image editors, and besides, I want to automate webcomic creation as much as possible. So I settled on running k-means clustering on the pixel values with k=2 clusters. This gives two clusters, one corresponding to the blacks and one corresponding to the whites in the image:

[![](/images/make-webcomics-easily-img-3.png "hist-hithere2")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/09/hist-hithere2.png)

Histogram of pixel values (0-255). Cluster of blacks on the left with centroid at 16. Whites on the right, centroid at 110.

The average of the two centroids can be taken to be the threshold. The threshold for the example above came out to be 63 — pretty far from 128! By the way, the mean pixel value is 103, which would clearly not have worked as well as the mean of the cluster centroids did.

This code may be useful to others who want to put up their comics/doodling on the web. Unfortunately, the program has a number of python module dependencies (Scipy, PyPNG, Numpy), because I just wanted a quick hack. But I’ll put up the code here anyway. Someday, I’ll get a github account.

```

import numpy, png, os, sys, pylab as plt
import scipy
from scipy.cluster.vq import vq, kmeans

infile = sys.argv[1]

print 'Converting to PNG...'
#Make sure input is a png
pngfile = infile.split('.')[0]+'.png'
os.system('convert ' + infile + ' ' + pngfile)

print 'Reading in pixels...'
f = open(pngfile, 'rb')
r = png.Reader(file=f)
k = r.read()
l = list(k[2])
numplanes = k[3]['planes']
l = zip(*l)
numrows = len(l)
l = l[0:numrows:numplanes] # This will skip every numplanes element
l = zip(*l)
f.close()

# Create a 1-D array of all the pixel values
l = numpy.array(l)
pixels = []
for i in range(0, len(l)):
	for j in range(0, len(l[0])):
		pixels.append(l[i][j])
pixels = numpy.array(pixels)

print 'Computing threshold...'
# Find the adaptive threshold by running one-dimensional k-means, with k = 2, and find the mean of the two cluster centers.
j = scipy.cluster.vq.kmeans(pixels, 2)
adaptivethreshold = (j[0][0] + j[0][1])/float(2)

print 'thresholding...'
# now threshold
for i in range(0, len(l)):
	for j in range(0, len(l[0])):
		if l[i][j] < adaptivethreshold:
			l[i][j] = 0
		else:
			l[i][j] = 255

print 'Writing to file...'
# Now write:
thresholdfile = pngfile.split('.')[0]+'-threshold.png'
f = open(thresholdfile, 'wb')
w = png.Writer(len(l[0]), len(l), greyscale = True)
w.write(f, l)
f.close()
```
