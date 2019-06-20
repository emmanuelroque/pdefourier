Fourier analysis provides a set of techniques for solving partial differential equations (PDEs) in both bounded and unbounded domains, and various types of initial conditions. In the bounded domain case, the method of separation of variables leads to a well-defined algorithm for developing the solution in a Fourier series, making this problem tractable with a CAS.

This Maxima package computes Fourier series symbolically for piecewise-smooth functions. Using the method of separation of variables it is able to solve symbolically the one-dimensional heat and wave equations on a domain \([0,L] \), with general boundary conditions of the form:
\begin{align*}
\alpha_1 u(0,t) + \beta_1 u_x(0,t)=f_1(t) \\
\alpha_2 u(L,t) + \beta_2 u_x(L,t)=f_2(t)
\end{align*}

Also, the package can solve the two-dimensional Laplace equation for a variety of domains (rectangles, disks, annuli, wedges) and Dirichlet and Neumann boundary conditions. Of course in all cases it is possible to truncate a series to make numerical calculations.

