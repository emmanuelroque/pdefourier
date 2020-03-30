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
 u<sub>t</sub>+&kappa; u<sub>xx</sub>=0, x&isin;[0,L], t>0 <br>
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
![Example 1](img/Example1.png?raw=true) 
<p align="left"> 
<code>(%i7)	kill(Q,F,h1,h2)$</code><br>
</p>

**Example 2** Consider the following problem for the wave equation in (x,t)&isin;[0,L] x [0,&infin;[:
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
![Example 2-1](img/Example2-1.png?raw=true) 
</p>
We can simplify the output a little bit:
<p align="left">
<code>(%i16)	factor(%);</code><br>
<code>(%o16)</code><br>
</p>
![Example 2-2](img/Example2-2.png?raw=true) 
Mathematica&trade; can not solve it, but Maple&trade; does. In case you want to compare the output
given here with that of Maple&trade;'s, please notice that
<p align="left">
<code>(%i17)	fouriersin_series((a*L^2*x-a*x^3)/6,x,L,inf);</code><br>
<code>(%o17)</code>
</p>
![Example 2-3](img/Example2-3.png?raw=true) 
<p align="left">
<code>(%i18)	kill(T,f,g,bb1,bb2)$</code><br>
</p>

 **Example 3** This is a  Neumann problem for the Laplace equation on a wedge defined by 0<&theta;<&pi;/2, 0<r<1:
<p align="left">
 &Delta;u=0 <br>
 u(r,0)=0=u(r,a) <br>
 u<sub>r</sub>(&theta;,r)= cos(4&theta;)<br>
</p>

The solution is readily found:

<p align="left">
<code>(%i19)	ur(theta):= if (0<=theta and theta<=%pi/2) then cos(4*theta)$</code><br>
<code>(%i20)	neumann_laplace_wedge(R,%pi/2,ur(theta),theta,inf);</code><br>
<code>The sum is over &#x2115;-{2}</code><br>
<code>(%o20)</code><br>
</p>
![Example 3](img/Example3.png?raw=true) 

To get a graphical representation of the solution, we can truncate the resulting series:

<p align="left">
<code>(%i21)	expr:neumann_laplace_wedge(1,%pi/2,ur(theta),theta,15)$</code><br>
<code>(%i22)	u_r1:at(diff(expr,r),r=1)$</code><br>
<code>(%i23)	draw3d(view=[67,151],surface_hide = true,</code><br>
<code>	       color = orange,</code><br>
<code>	       parametric_surface(r*cos(theta),r*sin(theta),expr,r,0,1,theta,0,%pi/2),</code><br>
<code>	       line_width  = 3,</code><br>
<code>	       color = blue,</code><br>
<code>	       parametric(t,0,0,t,0,1),</code><br>
<code>	       color = blue,</code><br>
<code>	       parametric(0,t,0,t,0,1)</code><br>
<code>	)$</code><br>
<code>(%t23)</code><br>	 
</p>
![Neumann problem for Laplace equation on a wedge](img/Neumann-Laplace.png?raw=true) 
