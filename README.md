**University of Pennsylvania, CIS 565: GPU Programming and Architecture,
Project 1 - Flocking**

* Eric Chiu
* Tested on: Windows 10 Education, Intel(R) Xeon(R) CPU E5-1630 v4 @ 3.60GHz 32GB, NVIDIA GeForce GTX 1070 (SIGLAB)

## Result

![](./images/Boids.gif)

## Performance Analysis

![](./images/Boids-FPS-With-Visualization.png)

![](./images/Boids-FPS-Without-Visualization.png)

As we can see from the graphs, when the number of boids increases, the frame rate and performance generally decreases for all implementations: naive, scattered, and coherent. This is probably because it is more likely to have more boids within a neighborhood distance. This means that we have to iterate over more boids in order to calculate the next position of a single boid.

There was performance improvements from the scattered uniform grid to the coherent uniform grid, but only by a small percentage (15% to 20%). I expected the outcome to be at least twice as fast. After thinking about it a little more, I realized that cutting out the middleman does make accessing data faster, but there are still roughly the same number of operations needed to calculate the next position of a single boid. Because of this, it made sense that performance was only by improved by 15% to 20%.

![](./images/Block-FPS-Without-Visualization.png)

When the block size increases from 16 to 32, the frame rate and performance is improved for all implementations: naive, scattered, and coherent. After we increase the block size further to 64, 128, and so forth, the performance generally is barely affected. I suspect the reason for this is because the warp size is set to 32.

Changing cell width and checking 27 vs 8 neighboring cells decreased the performance for all implementations. I suspect the reason for this is because the more neighboring cells are checked, the more neighboring boids must be checked to see if it is within a boid's neighborhood distance. 