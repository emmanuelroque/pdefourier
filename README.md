# pdefourier
## A package for solving partial differential equations in Maxima CAS

Fourier analysis provides a set of techniques for solving partial differential equations (PDEs) in both bounded and unbounded domains, and various types of initial conditions. In the bounded domain case, the method of separation of variables leads to a well-defined algorithm for developing the solution in a Fourier series, making this problem tractable with a CAS.

This Maxima package computes Fourier series symbolically for piecewise-smooth functions. Using the method of separation of variables it is able to solve symbolically the one-dimensional heat and wave equations on a domain [0,L], with general boundary conditions of the form:
<p align="center">
&alpha;<sub>1</sub>u(0,t) + &beta;<sub>1</sub>u<sub>x</sub>(0,t) = f<sub>1</sub>(t) <br>
&alpha;<sub>2</sub>u(L,t) + &beta;<sub>2</sub>u<sub>x</sub>(L,t) = f<sub>2</sub>(t)
</p>

Also, the package can solve the two-dimensional Laplace equation for a variety of domains (rectangles, disks, annuli, wedges) and Dirichlet and Neumann boundary conditions. In the case of a rectangular domain [0,a] x [0,b], the package can solve the Laplace equation with mixed boundary conditions of the form
<p align="center">
(1-&alpha;)u(x,0) + &alpha;u<sub>y</sub>(x,0) = f<sub>0</sub>(x), 0 &le; x &le; a<br>
(1-&beta;)u(x,b) + &beta;u<sub>y</sub>(x,b) = f<sub>b</sub>(x), 0 &le; x &le; a<br>
(1-&gamma;)u(0,y) + &gamma;u<sub>x</sub>(0,y) = g<sub>0</sub>(y), 0 &le; y &le; b<br>
(1-&delta;)u(a,y) + &delta;u<sub>x</sub>(a,y) = g<sub>a</sub>(y), 0 &le; y &le; b<br>
</p>
where &alpha;,&beta;,&gamma;,&delta; &isin; [0,1].

Of course, in all cases it is possible to truncate a series to make numerical calculations.

**Remark**: `pdefourier` automatically loads other packages, including `piecewise`, `draw`, `simplify_sum`, and `syntactic_factor`. The Maxima package `syntactic_factor` was written by Stavros Macrackis. Currently, `pdefourier` loads the files `piecewise` and `syntactic_factor` contained in this repository.
