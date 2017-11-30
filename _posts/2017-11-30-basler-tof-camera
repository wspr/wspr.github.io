---
layout: post
title:  "Basler ToF Camera vs Kinect v2"
date:   2017-11-30 16:50:48 +0930
categories: point-cloud
---

For the last couple of years I've been running some projects using Kinect v2 depth cameras
for taking scans of the human body.
Recently, the Kinect v2 sensor was discontinued and I've been looking into alternatives.

It *looks* like the [Intel RealSense D435](https://click.intel.com/intelr-realsensetm-depth-camera-d435.html)
will be a good replacement for a similar price-point, although I'm not entirely sure what
mechanism the Intel sensors use to measure the depth images.
It may not be entirely comparable to the Kinect v2, which uses a time-of-flight approach
to measuring pixel ‘distance’.

There are also some industrial time-of-flight depth cameras, including the
[Odos StarForm](http://www.odos-imaging.com/product/starform-3d-time-of-flight-camera/)
and the [Basler ToF Camera](https://www.baslerweb.com/en/products/cameras/3d-cameras/).
This kind of hardware tends to be an order of magnitude more expensive than consumer hardware.
I recently had the chance to borrow a Basler camera for a test run, and I was surprised by the results.

The Basler ToF Camera was nicer in every respect than the Kinect v2 in terms of its ruggedness,
interface options, customisation, programmability, and so on.
But a like-for-like comparison against the Kinect v2 showed far inferior point cloud quality.

At a distance of around 1.5m, I sat on a stool and took images of myself with the standard
settings with both the Kinect v2 and the Basler ToF Camera.
For the Kinect v2 I was using the [OpenKinect `libfreenect2` library](https://github.com/OpenKinect/libfreenect2) to capture a single point cloud.
For the Basler ToF Camera I used the example file `SavePointCloud.cpp` provided in the ‘Basler ToF Software’ distribution.

As can be seen in the results below, for our purposes the Basler ToF camera won't be appropriate
for the kind of work we're trying to do.
For industrial purposes where a depth camera is used in a larger industrial setting, I'm sure
the Basler ToF Camera is more the suitable; as I mentioned above, I found it a very robust
and useable piece of hardware.

<img src="scan-cmp-Data-Body.png" />

For our projects around scanning the human body, the search for our next depth camera continues.

