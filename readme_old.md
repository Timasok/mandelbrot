# Research topic

Get maximum optimization

Research the use of optimization flags.

Using intrinsic functions for optimization.


# Algorithm and software tools

Here is a picture of Mandelbrot fractal created by our program.

![Mandelbrot](img/Mandelbrot_set.png)

This algorithm is often used to estimate the computational speed of hardware.

Note:
SFML is used as a graphics library.

## Optimization results

What kinds of optimization were used in this work?
* SIMD-instructions, such as Intel SSE intrinsics.
* Compiler optimization flags such as -O2, -O3, -Ofast.

Note:
Our CPU(intel core i3) supports SSE and AVX2 intrinsics. We used vectors of type __m128 and __m128i.
We measured FPS of our algorithm using
>sf::Clock 

It is relevant to examine FPS in different computation modes. Here are the iterations of each mode:
1. Calculate the pixels of the picture.
2. Calculate the pixels of the picture and display them.
3. Repeatedly calculate the pixels of the picture and display them once.(Matan interupted my work)

The table below shows the FPS measured for different optimization modes. 

| Computation modes | No flags    |     -O2     |     -O3     |     -Ofast    |
| :---------------: | :----------:| :---------: | :---------: | :----------:  |
|    1 + no_sse     |  **6.15** (1x) | 11.1 (1.8x) | 11.2 (1.8x) |  11.6  (1.9x) |
|    2 + no_sse     |   1.43 (1x) | 1.81 (1.3x) | 1.77 (1.2x) |  1.65  (1.2x) |
|    1 + sse        |   8.62 (1x) | 39.6 (4,6x) | 40.3 (4.7x) | **42.6** (4.9x) |
<!-- | sse + vid    |   1.69   | 1.85 |  2.01  | 2.14   | -->

By comparing the first two rows of the table we can conclude that 2nd mode works significantly slow. The drawing process is much slower than calculation. Because of that 2 + sse launch is meaningless.
SIMD acceleration will not be noticeable. 
>K_no_draw = (FPS_in_1_row_max / FPS_in_2_row_max) = 11.6/1.81 = 6.4

Maximum coefficient per row characterizes acceleration that can be achieved with -O flags.
>K_o = 1.3
>K_o = 1.9
>K_o = 4.9

Values in bold characterize the acceleration of computing using SSE and -O optimizations simultaneously. 
>K_sse+o = 42.6/6.15 = 6.9.
 
The main goal of this project was achieved: we sped up the algorithm's work as fast as possible. Experiment shows that it's about 6.9 times