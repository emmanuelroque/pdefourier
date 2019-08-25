# pdefourier
## A package for solving partial differential equations in Maxima CAS

Fourier analysis provides a set of techniques for solving partial differential equations (PDEs) in both bounded and unbounded domains, and various types of initial conditions. In the bounded domain case, the method of separation of variables leads to a well-defined algorithm for developing the solution in a Fourier series, making this problem tractable with a CAS.

This Maxima package computes Fourier series symbolically for piecewise-smooth functions. Using the method of separation of variables it is able to solve symbolically the one-dimensional heat and wave equations on a domain [0,L], with general boundary conditions of the form:
<p align="center"><img src="https://github.com/emmanuelroque/pdefourier/blob/master/img/hw-mixbc.png" align=middle width=250pt height=60pt/></p>

Also, the package can solve the two-dimensional Laplace equation for a variety of domains (rectangles, disks, annuli, wedges) and Dirichlet and Neumann boundary conditions. In the case of a rectangular domain, the package can solve the Laplace equation with mixed boundary conditions of the form
<p align="center"><img src="https://github.com/emmanuelroque/pdefourier/blob/master/img/lmixbc.png" align=middle width=350pt height=110pt/></p>


Of course in all cases it is possible to truncate a series to make numerical calculations.

**Remark**: `pdefourier` automatically loads other packages, including `piecewise`, `draw`, `simplify_sum`, and `syntactic_factor`. The Maxima package `syntactic_factor` was written by Stavros Macrackis. Currently, `pdefourier` loads the files `piecewise` and `syntactic_factor` contained in this repository.
