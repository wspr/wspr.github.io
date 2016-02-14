---
layout: post
title:  "Surf-plotting scattered data in Matlab (or: Delaunay interpolation without a grid)"
date:   2015-05-29 13:08:42 +1030
categories: matlab
---
Matlab has a number of methods for interpolating data, both for data that is sampled on a regular grid and for data that is "scattered", or randomly distributed.

<h2>Surface plotting</h2>

Plotting surfaces over grid points is easy using Matlab's surf command, and interpolation of that data to get smoother plots is straightforward. For example,

<code>
[x,y,z] = peaks(10);
surf(x,y,z);
</code>

will plot:

<img src="delsurf/peaks.png" alt="peaks" width="300" height="240" />

Generally I recommend avoiding 3D plots, so in 2D (<code>view(2)</code>):

<img src="delsurf/peaks2d.png" alt="peaks2d" width="300" height="240" />

The variables <code>x</code> and <code>y</code> are 10x10 matrices defined by (the equivalent of) <code>[x,y]=meshgrid(linspace(-3,3,10))</code>, and <code>z</code> is the value at each point in (x,y) space.

If you have sampled data with non-uniform spacing, however, it's not as obvious how to plot that data. In this case your data would be organised with <code>x</code>, <code>y</code>, and <code>z</code> as column vectors with each measurement per row. The structure of the <code>surf</code> command simply doesn't handle data in this form, since the data isn't organised in a way that allows adjacent points to be connected.

Matlab provides commands for analysing this data using Delaunay Triangulation, for which it also provides an analogue to <code>surf</code>. Here's an example:

<code>
N = 15;
rng(13); % repeatable random values
x = randn(1,N); % X &amp; Y coords
y = randn(1,N);
z = randn(1,N); % "value" at each coordinate
</code>

After a little digging, you'll find that the easiest way to plot this data as a surface is:

<code>
trisurf(delaunay(x,y),x,y,z)
</code>

Seems slightly redundant, but easy enough.

<h2>Surf plots with coarse grids</h2>

The problem is that surface plots are poor at visualising data over coarse meshes, since it's their corners which define the values. This can be seen in the following example, using <code>peaks</code> to plot a surface:

<img src="delsurf/meshgrid.png" alt="meshgrid" width="660" height="495" />

The first row shows plain <code>surf</code>. It can be seen that the colours of each "patch" don't do a good job of representing their height (or "value"). In the second row, Matlab's interpolating shader is used to "improve" this. It's an improvement, but distortions are obvious where there are large changes in both directions. (Colours are smeared along diagonals, basically.)

Finally, in the third row an interpolation function is used to generate more data points. This is quite a coarse interpolation, but couldn't go finer without the edges taking over in the 3D plot. The plot looks far more convincing. Gridded interpolation can be done in a number of ways; for this example I used

<code>
F = griddedInterpolant(x',y',z');
[x2,y2] = ndgrid(linspace(-3,3,20));
surf(x2,y2,F(x2,y2))
</code>

(The transpose being necessary from coordinates output from <code>peaks</code>. Good old Matlab.)

<h2>Surf plots with coarse scattered data</h2>

But what about scattered data? While Matlab does provide <code>scatteredInterpolant</code>, this form is only really convenient if you want to interpolate onto a regular grid. What if you just want to improve the look of your overly-coarse surface plot? Here's the example using trisurf described above, with and without interpolated shading (<code>shading interp</code>):

<img src="delsurf/delaunay1.png" alt="delaunay" width="660" height="495" />

Note that without the interpolated shading, the plot is basically unusable. But even with interpolated shading, there's significant distortion along certain diagonals. I've left out the edge lines in the bottom-right graph to emphasise this. If we resampled this function over a regular grid using <code>scatteredInterpolant</code>, we'd end up with points outside the original region, which might not always be appropriate. We could then delete the outsiders, but that would require additional processing. Wouldn't it be nice to simply resample within the original?

<h2>Delaunay interpolation</h2>

To do this requires a couple steps. First, extract the Delaunay Triangularisation of our points:

<code>
DT = delaunay(x,y);
</code>

This function returns a list of 3xM indices into x and y, where M is the number of triangles. So if we extract the coordinates for each triangle and average them, we obtain the mid-point of each, including an interpolated value:

<code>
x2 = mean(x(DT),2);
y2 = mean(y(DT),2);
z2 = mean(z(DT),2);
</code>

This figure shows the grid that results after interpolating once and re-applying the Delaunay Triangularisation: (black before, red after)

<img src="delsurf/del01.png" alt="del01" width="300" height="225" />

Note that the Delaunay algorithm doesn't simply divide up the triangles into smaller components. We can then perform this iteratively to interpolate to an arbitrary level of detail:

<img src="delsurf/delinterp.png" alt="delinterp" width="660" height="495" />

And after removing the grid lines and increasing the order, the results look pretty nice:

<img src="delsurf/delinterp2.png" alt="delinterp2" width="660" height="495" />

Interpolation will never solve the problem of under-sampling if there's information missing, but it definitely helps to draw more pleasing figures.

I've uploaded this code to the Matlab file exchange under the name <a href="http://www.mathworks.com/matlabcentral/fileexchange/51117-delaunay-surf">delaunay_surf</a>, and added it to my generic Matlab repository on Github: <a href="https://github.com/wspr/matlabpkg">https://github.com/wspr/matlabpkg</a>. It's pretty basic:

<code>
p = delaunay_surf(x,y,z,'N',4);
</code>

with a few additional options. Check out the example file for more, er, examples.

Happy plotting!

