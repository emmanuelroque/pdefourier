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
where &alpha;,&beta;,&gamma;,&delta; &isin; {0,1}.

Of course, in all cases it is possible to truncate a series to make numerical calculations.

**Remark**: `pdefourier` automatically loads other packages, including `piecewise`, `draw`, `simplify_sum`, and `syntactic_factor`. The Maxima package `syntactic_factor` was written by Stavros Macrackis. Currently, `pdefourier` loads the files `piecewise` and `syntactic_factor` contained in this repository.

**Example 1** Consider the problem
<p align="left">
 u<sub>t</sub>+&kappa; u<sub>xx</sub>=0 <br>
 u(x,0)=1-x<sup>3</sup>/4<br>
 u<sub>x</sub>(0,t)=0<br>
 u<sub>x</sub>(1,t)=-u(1,t)<br>
</p> 

Physically, this corresponds to the heat propagation in a bar where the left end is insulated, and
the right end has convection heat loss.

We solve it with the following commands:
<p align="left">
<code>(%i1)	load(pdefourier)$</code><br>
<code>(%i2)	Q(x,t):=if (0<=x and x<=1) then 0$</code><br>
<code>(%i3)	F(x):=if (0<=x and x<=1) then 1-x^3/4$</code><br>
<code>(%i4)	h1(t):=0$</code><br>
<code>(%i5)	h2(t):=0$</code><br>
<code>(%i6)	mixed_heat(Q(x,t),F(x),0,1,1,1,h1(t),h2(t),x,t,1,k,inf);</code><br>
<code>(%o6)	%lambda[n] are the solutions of %lambda[n]*cos(%lambda[n])-%lambda[n]^2*sin(%lambda[n])=0</code><br>
<a href="https://www.codecogs.com/eqnedit.php?latex=3&space;\sum_{n=1}^\infty&space;\[\frac{\left(&space;{{\lambda&space;}_n}\,&space;\left(&space;{{\lambda&space;}_{n}^{2}}&plus;2\right)&space;\sin{\left(&space;{{\lambda&space;}_n}\right)&space;}-\left(&space;{{\lambda&space;}_{n}^{2}}-2\right)&space;\cos{\left(&space;{{\lambda&space;}_n}\right)&space;}-2\right)&space;\,&space;{e^{-k\,&space;{{\lambda&space;}_{n}^{2}}&space;t}}&space;\cos{\left(&space;{{\lambda&space;}_n}&space;x\right)&space;}}{{{\lambda&space;}_{n}^{3}}\,&space;\left(&space;\sin{\left(&space;2&space;{{\lambda&space;}_n}\right)&space;}&plus;2&space;{{\lambda&space;}_n}\right)&space;}\]" target="_blank"><img src="https://latex.codecogs.com/svg.latex?3&space;\sum_{n=1}^\infty&space;\[\frac{\left(&space;{{\lambda&space;}_n}\,&space;\left(&space;{{\lambda&space;}_{n}^{2}}&plus;2\right)&space;\sin{\left(&space;{{\lambda&space;}_n}\right)&space;}-\left(&space;{{\lambda&space;}_{n}^{2}}-2\right)&space;\cos{\left(&space;{{\lambda&space;}_n}\right)&space;}-2\right)&space;\,&space;{e^{-k\,&space;{{\lambda&space;}_{n}^{2}}&space;t}}&space;\cos{\left(&space;{{\lambda&space;}_n}&space;x\right)&space;}}{{{\lambda&space;}_{n}^{3}}\,&space;\left(&space;\sin{\left(&space;2&space;{{\lambda&space;}_n}\right)&space;}&plus;2&space;{{\lambda&space;}_n}\right)&space;}\]" title="3 \sum_{n=1}^\infty \[\frac{\left( {{\lambda }_n}\, \left( {{\lambda }_{n}^{2}}+2\right) \sin{\left( {{\lambda }_n}\right) }-\left( {{\lambda }_{n}^{2}}-2\right) \cos{\left( {{\lambda }_n}\right) }-2\right) \, {e^{-k\, {{\lambda }_{n}^{2}} t}} \cos{\left( {{\lambda }_n} x\right) }}{{{\lambda }_{n}^{3}}\, \left( \sin{\left( 2 {{\lambda }_n}\right) }+2 {{\lambda }_n}\right) }\]" /></a>
<p align="left"> 
<code>(%i7)	kill(Q,F,h1,h2)$</code><br>
</p>

**Example 2** Consider the following problem for the wave equation
<p align="left">
 u<sub>tt</sub>=c<sup>2</sup> u<sub>xx</sub>+ax <br>
 u(L,0)=0=u(0,t)<br>
 u<sub>x</sub>(0,t)=0<br>
 u<sub>t</sub>(x,0)=0=u(x,0)<br>
</p> 

This is Example 4.31 in J. D. Logan's ''Applied Partial Differential Equations'' (3rd. Ed.), Springer Verlag, 2015.

The following Maxima session solves it:

<p align="left">
<code>(%i8)	assume(t>0)$</code><br>
<code>(%i9)	assume(L>0)$</code><br>
<code>(%i10)	T(x,t):=if (0<=x and x<=L) then a*x$</code><br>
<code>(%i11)	f(x):=if (0<=x and x<=L) then 0$</code><br>
<code>(%i12)	g(x):=if (0<=x and x<=L) then 0$</code><br>
<code>(%i13)	bb1(t):=0$</code><br>
<code>(%i14)	bb2(t):=0$</code><br>
<code>(%i15)	mixed_wave(T(x,t),f(x),g(x),1,0,1,0,bb1(t),bb2(t),x,t,L,c,inf);</code><br>
<code>(%o15)</code><br>
  <a href="https://www.codecogs.com/eqnedit.php?latex=\frac{1}{\pi^3&space;c^2}&space;\sum_{n=1}^{\infty&space;}{\left.&space;\frac{\left(&space;2&space;{{L}^{3}}&space;a\,&space;{{\left(&space;-1\right)&space;}^{n}}&space;\cos{\left(&space;\frac{\ensuremath{\pi}&space;c&space;n&space;t}{L}\right)&space;}-2&space;{{L}^{3}}&space;a\,&space;{{\left(&space;-1\right)&space;}^{n}}\right)&space;\sin{\left(&space;\frac{\ensuremath{\pi}&space;n&space;x}{L}\right)&space;}}{{{n}^{3}}}\right.}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\frac{1}{\pi^3&space;c^2}&space;\sum_{n=1}^{\infty&space;}{\left.&space;\frac{\left(&space;2&space;{{L}^{3}}&space;a\,&space;{{\left(&space;-1\right)&space;}^{n}}&space;\cos{\left(&space;\frac{\ensuremath{\pi}&space;c&space;n&space;t}{L}\right)&space;}-2&space;{{L}^{3}}&space;a\,&space;{{\left(&space;-1\right)&space;}^{n}}\right)&space;\sin{\left(&space;\frac{\ensuremath{\pi}&space;n&space;x}{L}\right)&space;}}{{{n}^{3}}}\right.}" title="\frac{1}{\pi^3 c^2} \sum_{n=1}^{\infty }{\left. \frac{\left( 2 {{L}^{3}} a\, {{\left( -1\right) }^{n}} \cos{\left( \frac{\ensuremath{\pi} c n t}{L}\right) }-2 {{L}^{3}} a\, {{\left( -1\right) }^{n}}\right) \sin{\left( \frac{\ensuremath{\pi} n x}{L}\right) }}{{{n}^{3}}}\right.}" /></a>
</p>
We can simplify the output a little bit:
<p align="left">
<code>(%i16)	factor(%);</code><br>
<code>(%o16)</code><br>
</p>
<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{2L^3a}{\pi^3&space;c^2}\sum_{n=1}^{\infty&space;}{\left.&space;\frac{{{\left(&space;-1\right)&space;}^{n}}\,&space;\left(&space;\cos{\left(&space;\frac{\ensuremath{\pi}&space;c&space;n&space;t}{L}\right)&space;}-1\right)&space;\sin{\left(&space;\frac{\ensuremath{\pi}&space;n&space;x}{L}\right)&space;}}{{{n}^{3}}}\right.}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\frac{2L^3a}{\pi^3&space;c^2}\sum_{n=1}^{\infty&space;}{\left.&space;\frac{{{\left(&space;-1\right)&space;}^{n}}\,&space;\left(&space;\cos{\left(&space;\frac{\ensuremath{\pi}&space;c&space;n&space;t}{L}\right)&space;}-1\right)&space;\sin{\left(&space;\frac{\ensuremath{\pi}&space;n&space;x}{L}\right)&space;}}{{{n}^{3}}}\right.}" title="\frac{2L^3a}{\pi^3 c^2}\sum_{n=1}^{\infty }{\left. \frac{{{\left( -1\right) }^{n}}\, \left( \cos{\left( \frac{\ensuremath{\pi} c n t}{L}\right) }-1\right) \sin{\left( \frac{\ensuremath{\pi} n x}{L}\right) }}{{{n}^{3}}}\right.}" /></a>

Mathematica&trade; can not solve it, but Maple&trade; does. In case you want to compare the output
given here with that of Maple&trade;'s, please notice that
<p align="left">
<code>(%i17)	fouriersin_series((a*L^2*x-a*x^3)/6,x,L,inf);</code><br>
<code>(%o17)</code>
</p>
<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{2&space;{{L}^{3}}&space;a\,&space;\sum_{n=1}^{\infty&space;}{\left.&space;\frac{{{\left(&space;-1\right)&space;}^{n&plus;1}}&space;\sin{\left(&space;\frac{\ensuremath{\pi}&space;n&space;x}{L}\right)&space;}}{{{n}^{3}}}\right.}}{{{\ensuremath{\pi}&space;}^{3}}}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\frac{2&space;{{L}^{3}}&space;a\,&space;\sum_{n=1}^{\infty&space;}{\left.&space;\frac{{{\left(&space;-1\right)&space;}^{n&plus;1}}&space;\sin{\left(&space;\frac{\ensuremath{\pi}&space;n&space;x}{L}\right)&space;}}{{{n}^{3}}}\right.}}{{{\ensuremath{\pi}&space;}^{3}}}" title="\frac{2 {{L}^{3}} a\, \sum_{n=1}^{\infty }{\left. \frac{{{\left( -1\right) }^{n+1}} \sin{\left( \frac{\ensuremath{\pi} n x}{L}\right) }}{{{n}^{3}}}\right.}}{{{\ensuremath{\pi} }^{3}}}" /></a>
<p align="left">
<code>(%i18)	kill(T,f,g,bb1,bb2)$</code><br>
</p>
