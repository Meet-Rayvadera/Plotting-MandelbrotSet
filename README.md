# Plotting Mandelbrot Set
Plotting Mandelbrot set is computationally heavy problem. We implemented it using shared memory parallelism with OpenMP interface. This repository contains code, results, presentation of project.

# Introduction
Mandelbrot set is fractal structure, which is set of complex numbers c for which sequence z_{n+1} = z_n^2+ c does not diverge, when iterated from z1 = 0. Plot can be obtained by sampling complex plane according to pixel of image which we want to generate and then coloring that point according to how rapidly it converges. Black color will denote that point will belong to set and white point will denote point doesn't belong to set because for that point sequence is diverging. We have set bound of 2, so for any point to be in set, absolute value of terms of sequence should be less than 2.

# Brief description about Serial Implementation
For plotting Mandelbrot set on complex plane, we have to check sequence for each point (starting from that point) in complex plane, whether sequence remains bounded in absolute value or not. So for that we first have to iterate through all points of plane, number of points will be specified from input(n). We will fix the range of complex plane, -2 to 1 on X-axis and -1.5 to 1.5 on Y-axis. Number of terms in particular sequence for each point is taken to be 120. So for each point, max iterations would be 120. For sequence of each point, if sequence fells outside circle of radius 2 then there won't be need to calculate further terms of sequence. Now we have to decide the color for each point such that it tells us about how much sequence for that particular point remains in bound. For that first normalize number of iteration till when it remained in bound to 0 to 255. We want to show zero color for unboundedness and black color for boundedness. So subtract that number from 255. Now give this number to R,G,B values differently to get different patterns for points where iterations are neither too small nor too big. Finally after deciding R,G,B values for each point, put it on the plot.

# Brief description about Parallel Implementation
We will have computation for each point, so we will divide number of rows into different cores by inserting Pragma on outer loop. Here we have to declare iterating variables to be private and Number of Iterations array and PPM image to be shared (So each thread can access it).
Number of points divided between cores would be almost equal but number of iterations for each point might be different (as iterations will be stopped once value goes out of bound.)

