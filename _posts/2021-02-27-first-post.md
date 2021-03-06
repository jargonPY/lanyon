---
layout: post
mathjax: true
title: "From Heat to Sound Part I: Deriving the Fourier Series"
---

The Fourier Series is a concept of profound importance to mathematics but also physics and engineering.  Notwithstanding the importance of the Fourier series, it is often presented in a matter of fact fashion that shrouds the concept in some mystery. In attempt to demystify the Fourier series many have published great articles that help develop intuition behind the idea, which I highly recommend. For my self I found that understanding the history of ideas, the problems it attempted to solve provides a unique perspective. More importantly it shines a light on the process of discovery in mathematics, and it reveals the struggles of the individuals as they were battling with these ideas.

Unlike some other great resources in this series of articles I will focus on deriving the Fourier series, the Fourier transform and their discrete counterparts. It seems that most places I looked the formulas were presented with little justification or explanation between their relationships. I have decided to explore these relationships and what I found will be presented here.

This article will be the first of a three part series:

### Part I:<br>
In this article I'll attempt to walk through a plausible derivation of the Fourier series. By plausible I mean I don't necessarily follow Fourier's derivation but rather I will start by solving the same problem he was intrested in and thus the derivation is inspired by historically accurate events.

Hopefully by following through the derivation you will be able to see the logical connections
between concepts rather than percieve them as a disjoint set of ideas.

### Part II:<br>
Here I will present a derivation of the Discrete Fourier Transform. Since most modern applications of the Fourier transform are within the digital domain this part is crucial to understand the intracies of converting the continous F.T. to the Discrete version (I will not cover the Fast Fourier Transform as there are great resources online already available for that)

### Part III:<br>
In this final section I will explore some applications of the Discrete Fourier Series and the Fourier Transform.

## Disclaimer
Admittely to fully grasp the concepts that will be presented in this series of articles a little background in partial differential equations and complex numbers will be necessary. I will avoid questions of convergence and the existence of certain limits and just provide a plausible derivation (by making many assumptions along the way). After all Fourier did not prove his results but rather used them simply because they worked. 

I will try to show most steps in the derivation. At times this may lead
to a rather daunting presentation as there will be a fair amount of algebraic manipulations, nevertheless I believe the benefits of following every step justify the presentation.

Finally I would recommend spending some time with the ideas presented, exploring where some thoughts take you, after all that is the process of discovery.

## Very Brief History:

The Fourier series was first proposed in 1807 by Joseph Fourier while he 
was studing the propogation of heat in solid bodies. At the dawn of 19th
century heat was a poorly understood concept (this was before thermodynamics), and
although heat itself might not have been understood there was an equation that
descried its motion. Somewhat unimaginatevly this equation is known as the heat 
equation and it descibes the flow of heat across some surface. 
Just like Fourier did, we will solve the heat equation and be able to see how he arrived at the infamous series. 

## Solving the Heat Equation:

To begin lets introduce the (1-D) heat equation:

$$
k\frac{\partial^2 T}{\partial x^2} = \frac{\partial T}{\partial t}
\tag{1}
$$

Here $$T$$ represents the temperature and $$k$$ is the thermal conductivity of the material (the material's ability to conduct heat). Imagine a thin rod of some length $$L$$, by specifying the temperature at every point on the rod at some point in time (we'll call this point $$t=0$$), by solving this equation we will be able to predict the temperature at point on the rod in the future, and thus this equation tells us how heat flows across the rod.

Let's define an initial temperature distribution:

$$
T(x, 0) = f(x)
$$

and the boundary conditions

$$
T(0,t) = T(L,t) = 0
$$

Now that we got everything in place, lets solve. Notice that $$x$$ only occurs on one side of the equation and $$t$$ only on the other. Differential equations of this form can be solved with a technique knwon as seperation of variables. This just means that we'll assume that our solution takes the following form:

$$
T(x,t) = f(x)g(t)
\tag{2} 
$$

We know plug $$(2)$$ into the heat equation $$(1)$$:

$$
k\frac{\partial^2 f(x)g(t)}{\partial x^2}=\frac{\partial f(x)g(t)}{\partial t}
$$

Since $$g(t)$$ is independent of $$x$$ and $$f(x)$$ is independent of $$t$$, we can rearrange the eqution to get:

$$
k\frac{f^{''}(x)}{f(x)}= \frac{g^{'}(t)}{g(t)} = -m
\tag{3}
$$

Where  did the $$(-m)$$ come from? Well notice that the left side of the equation is a function of $$x$$ and the right hand side is only a function of $$t$$. Perhaps rewriting it can make it clearer:

$$
kF(x)=G(t)
$$

The only way the equation above holds is if is if both functions are constant.

By rearranging $$(3)$$ and solving each equation separately, we see that we have two seperate ordinary differential equations to solve:

$$
g(t) = -mg(t)\\[2ex]
f^{''}(x) = -\frac{m}{k}f(x)\\[2ex]
$$

The solutions are:

$$
g(t) = Ce^{-mt}\\[2ex]
f(x) = \sin{(\sqrt{\frac{m}{k}}x)}
$$

Recall we assumed that $$T(x,t)=f(x)g(t)$$. Since we just solved for $$f(x)$$ and $$g(t$)$ we have our solution for $$T$$!

$$
T(x,t)=Ce^{-mt}\sin{(\sqrt{\frac{m}{k}}x)}
$$

Alright so now that we have our equation how do we figure out the value of $$m$$? Well that constant depends on the physical system we want to model and can be solved for by using our boundary conditions.

$$
T(L,t) = Ce^{-mt}\sin(\sqrt{\frac{m}{k}}L) = 0
$$

Since we don't want to solve for a trivial solution where our temperature is always zero across the rod, We'll assume $$C\neq 0$$ and thus it means that 

$$
\sin(\sqrt{\frac{m}{k}}L) = 0\\[2ex]
\sqrt{\frac{m}{k}}L = nπ\\[2ex]
m = k(\frac{nπ}{L})^2
$$

Seeing that any value of $$n$$ satisfies our equation, by principle of superposition we get our general solution:

$$
T(x,t)=\sum_{n=0}^{∞}C_ne^{-k(\frac{nπ}{L})^2t}\sin{({\frac{nπ}{L}}x)}
$$

Great so we've done all this work but what does this have anything to do with the Fourier series? Lets look closer at our equation when $$t=0$$

$$
T(x,0)=\sum_{n=0}^{∞}C_n\sin{({\frac{nπ}{L}}x)} = f(x)
$$

What's going on there? Well we see that some function $$f(x)$$ is defined as a sum of sinusoidal functions. This is percisely the Fourier series. But lets review. Recall that $$f(x)$$ in our problem represents the temperature distribution over the rod. Since we have not placed any restrictions on the function (except for the boundaries), this function can be anything we'd like, and it seems that this arbitrary function can be represted by the sum of sinusoidal functions. So what does that mean?

At first glance we may be tempted to say that *any* function can be decomposed into an infinite sum of sines. But we know there are boundary conditions so maybe we limit ourselves to *any* function that is zero at the boundaries? Well lets explore this intuition.

Notice the form of $$f^{''}(x) = -(\frac{m}{k})f(x)$$, both cosine and sine are valid solutions. Recall the reason we chose sine is so that our boundary conditions are satisfied at $$x=0$$. Given a different boundary condition we might have chosen cosine and stated that any distribution can also be represented by an infinite sum of cosine functions. This makes the matter even more confusing. We see that some functions may be expanded into a sum of cosines others into a sum of sines. How do we know which functions belong to which class?

To answer these ambiguities we need to see if we can find any restrictions that arise by using trigonometric functions in our expansion.

### Restriction I: Parity of $$f$$ (Even or Odd?)
Recall that sine is an odd function, which means that $$\sin(-x)=-\sin(x)$$. It turns out that the sum of odd functions is also an odd function, and since $$f(x)$$ is a sum of sines it itself must also be odd. Here is a quick proof:

$$
f(-x)=\sum_{n=0}^{∞}C_n\sin{(-{\frac{nπ}{L}}x)}\\[2ex]
=-\sum_{n=0}^{∞}C_n\sin{({\frac{nπ}{L}}x)}\\[2ex]
=-f(x)
$$

As for cosines they are even functions, that is $$\cos(-x)=\cos(x)$$. Following the same chain of reasoning we know that the sum of even functions must also be even.
The same reasoning hold for cosine functions.

So we have found one limitation of our expansion, namely if we use sines we can only
represent odd functions and if we use cosines, only even functions can be represented.
We will overcome this restriction soon but for now let us proceed.

### Restriction 2: Periodicity
Recall that sines and cosines are periodic functions. So perhaps a superposition of these functions must also be periodic? Lets see.<br>

Let us dissect the components of the sine function $$\sin⁡(\frac{nπ}{L}x)$$, here $$\frac{nπ}{L}$$ represents the angular frequency $$ω=nπ/L$$ and the period is given by $$P=\frac{2π}{ω}=\frac{2L}{n}$$. Notice that as $$n$$ increases the period gets shorter but remains a constant multiple of $$2L$$, which is known as the fundamental frequency. 
Lets develop this intuition, while $$\sin⁡(\frac{π}{L}x)$$ completes one cycle $$\sin⁡(\frac{2π}{L}x)$$ completes two cycles, but their superposition $$f(x)=\sin⁡(\frac{π}{L}x)+\sin⁡(\frac{2π}{L}x)$$ only repeats when both repeat.
Therefore,

$$
f(x+2L)=\sum_k \sin(\frac{nπ}{L}(x+2L))\\[2ex]
=\sum_k \sin(\frac{nπ}{L}x+2nπ))\\[2ex]
=\sum_k \sin(\frac{nπ}{L}x)\\[2ex]
=f(x)
$$

Overcoming Restriction 1:
So we have seen that a sine and cosine expansions can perhaps represent odd and even periodic function respectively. What about functions that are neither odd nor even?

Well we might be able to represent these that are neither odd nor even as a superposition of even and odd functions

$$
f(-x)=\sum_k \sin(-kx) + cos(-kx)\\[2ex]
=\sum_k -\sin(kx)+cos(kx)
$$

In this case $$f(x)$$ is neither even nor odd. 
We have shown that a superposition of an even and odd function results in a function that is neither even nor odd. Notice however that we have not proved that any function can be represented as a series expansion of sines and cosines. This minor inconvenience did not stop Fourier from proposing that such an expansion exists for all periodic functions, which was the birth of the Fourier series.

$$
f(x)=\sum_{n=0}^∞ A_n\cos(\frac{nπ}{L}x) + B_n\sin(\frac{nπ}{L}x)
\tag{4} 
$$

This proposition stressed the lack of rigor in the study of analysis (a field that deals with limits, convergence etc.) at the turn of the 19th century and lead several mathematicians into the development a rigorous foundation of analysis. Particularly questions of convergence and whether or not discontinuous functions be represented by continuous functions.

## Finding the Coefficients: 

Assuming we accept the idea that our function can be composed by an arbitrary combination of sines and cosines, what now? Without knowing the coefficients $$A_n$$ and $$B_n$$, this whole endeavor remains nothing more than a mathematical curiosity. Luckily these trigonometric functions have an extremely useful property that we can exploit to determine our coefficients.

First let us define orthogonal functions. Two functions are orthogonal if the following holds $$∫f(x)g(x)dx=0$$. Note this is a definition, meaning we do not prove it but rather state that any two functions that satisfy this property will be called orthogonal. The next two properties is what allows us to find the Fourier expansion of a function (I will not go through the integration as this is not the focus of this article):

$$
∫\cos⁡(nx)\sin⁡(mx)dx=0 \\[2ex]
∫\cos⁡(nx)\cos⁡(mx)dx= 
\begin{cases}
1,  & \text{if $m=n$} \\
0, & \text{if $m\neq n$}
\end{cases}
$$

Using the orhogonality of the trigonometric functions we can proceed to find our coefficients. To find $$A_m$$, we multiply both sides of $$(4)$$ by $$\cos⁡(\frac{nπ}{L} x)$$ and integrate over a single period from $$-\frac{T}{2}$$ to $$\frac{T}{2}$$

$$
\int_{-\frac{T}{2}}^\frac{T}{2}f(x)\cos⁡(\frac{mπ}{L}x)dx=\int_{-\frac{T}{2}}^\frac{T}{2}\cos⁡(\frac{mπ}{L}x)[\sum_{n=0}^∞ A_n\cos(\frac{nπ}{L}x) + B_n\sin(\frac{nπ}{L}x)]dx
$$

By distributing the cosine term and interchanging the sum an the integral (we'll assume that the order is interchangeable):

$$
\int_{-\frac{T}{2}}^\frac{T}{2}f(x)\cos⁡(\frac{mπ}{L}x)dx \\[2ex]
=\sum_{n=0}^∞ \int_{-\frac{T}{2}}^\frac{T}{2}A_n\cos(\frac{nπ}{L}x)\cos(\frac{mπ}{L}x)dx+
\sum_{n=0}^∞ \int_{-\frac{T}{2}}^\frac{T}{2}B_n\sin(\frac{nπ}{L}x)\cos(\frac{mπ}{L}x)dx
$$

All terms are equal to zero by orthogonally of sines and cosines except one, where $$m=n$$:

$$
\int_{-\frac{T}{2}}^\frac{T}{2}f(x)\cos⁡(\frac{nπ}{L}x)dx=\frac{T}{2}A_n \\[2ex]
A_n=\frac{2}{T} \int_{-\frac{T}{2}}^\frac{T}{2}f(x)\cos⁡(\frac{nπ}{L}x)dx
$$

Now if instead of multiplying by cosine we multiply by sine and follow the same steps we get our second coefficient

$$
B_n=\frac{2}{T} \int_{-\frac{T}{2}}^\frac{T}{2}f(x)\sin(\frac{nπ}{L}x)dx
$$

There are many approaches to understanding the Fourier series, each of which highlights a different perspective and interpretation. But one of the most common ways to describe the role of the coeffcients is that they represent the amplitudes of their respective frequencies 
$$f=\frac{ω_n}{2π}=\frac{nπ}{L}\frac{1}{2π}=\frac{n}{2L}$$

## Rewriting the Fourier Series Using Complex Notation: 
Now that we have finished deriving the Fourier series we are left with two basic questions, how do we overcome our limitation of representing only periodic functions and how is the Fourier series related to the Fourier transform? It turns out that the Fourier transform is the solution to our periodicity problem, to see that and how we get there we must first rewrite the Fourier series using complex notation.
Recall Euler’s formula:

$$
Ce^{ix}=A\cos(x)+iB\sin(x)
$$

Notice however that the $$\sin$$ term is complex, whereas the Fourier series $$(4)$$ has no complex components. To remedy the situation we can make use of some useful identities:

$$
\cos(x) = \frac{e^{ix}+e^{-ix}}{2} \\[2ex]
\sin(x) = \frac{e^{ix}-e^{-ix}}{2i} 
$$

Using the above identities we get the following result:

$$
A_n\cos(nx) + B_n\sin(nx) = A_n\frac{e^{inx}+e^{-inx}}{2} + B_n\frac{e^{inx}-e^{-inx}}{2i} \\[2ex]
$$

Rearraning the terms on the right hand side we get:

$$
A_n\frac{e^{inx}+e^{-inx}}{2} + B_n\frac{e^{inx}-e^{-inx}}{2i} = \frac{(iA_n+B_n)e^{inx}}{2i} + \frac{(iA_n-B_n)e^{inx}}{2i}
\tag{5}
$$

Lets define the coefficent for the first exponential $$C_n$$:

$$
C_n = \frac{(iA_n+B_n)}{2i} = \frac{A_n}{2} + \frac{B_n}{2i}
$$

Now recall the definitions of $$A_n$$ and $$B_n$$ and notice what happens if we change $$n$$ to a negative integer:

$$
A_{-n} = \frac{2}{T} \int_{-\frac{T}{2}}^\frac{T}{2}f(x)\cos⁡(-nx)dx \\[2ex]
=\frac{2}{T} \int_{-\frac{T}{2}}^\frac{T}{2}f(x)\cos⁡(nx)dx \\[2ex]
= A_n \\[2ex]

B_{-n} = \frac{2}{T} \int_{-\frac{T}{2}}^\frac{T}{2}f(x)\sin(-nx)dx \\[2ex]
=-\frac{2}{T} \int_{-\frac{T}{2}}^\frac{T}{2}f(x)\sin(nx)dx \\[2ex]
= -B_n
$$

So we see that $$A_{-n}=A_n$$ and $$B_{-n}=-B_n$$, that is $$A_n$$ is even and $$B_n$$ is odd. Now notice what happens when we plugin $$-n$$ into $$C_n$$:

$$
C_{-n} = \frac{A_{-n}}{2} + \frac{B_{-n}}{2i} \\[2ex]
C_{-n} = \frac{A_n}{2} - \frac{B_n}{2i}
$$

Which is the coefficient for the second exponential we got in equation $$(5)$$. And so we have arrived at a representation of our purely real series in terms of complex exponentials.

$$
C_ne^{inx} + C_{-n}e^{-inx} = A_n\cos(nx) + B_n\sin(nx)
$$

And the full Fourier series using complex exponentials:

$$
\sum_{-∞}^∞ C_ne^{i\frac{nπ}{L}x} = \sum_{n=0}^∞ A_n\cos(\frac{nπ}{L}x) + B_n\sin(\frac{nπ}{L}x)
$$


## The Fourier Transform: Overcoming Periodicity

Now we will venture into the Fourier transform, in fact we are already almost there. In the previous section we have found that

$$
C_{n} = \frac{A_{n}}{2} + \frac{B_{n}}{2i}
$$

Let's write it in fully in terms of the integrals

$$
C_n = \frac{1}{2}(\frac{2}{T} \int_{-\frac{T}{2}}^\frac{T}{2}f(x)\cos⁡(\frac{nπ}{L}x)) + \frac{1}{2i}(\frac{2}{T} \int_{-\frac{T}{2}}^\frac{T}{2}f(x)\sin(\frac{nπ}{L}x))dx \\[2ex]

C_n = \frac{1}{T}\int_{-\frac{T}{2}}^\frac{T}{2}f(x)[\cos⁡(\frac{nπ}{L}x) + i\sin(\frac{nπ}{L}x)]dx \\[2ex]

C_n = \frac{1}{T}\int_{-\frac{T}{2}}^\frac{T}{2}f(x)e^{i\frac{nπ}{L}x}dx
$$

We could also rewrite our fundamental angular frequency term $\frac{π}{L}$ in terms of the period $$T$$.

$$
w = \frac{π}{L} = 2πf = \frac{2π}{T}
$$

So $$C_n$$ becomes:

$$
C_n = \frac{1}{T}\int_{-T/2}^{T/2} f(x) e^{2πi(n/T)x}dx
\tag{6}
$$

To extend the domain of Fourier analysis to non-periodic functions we come up with a rather clever concept. We assume that the period of the function is inifinitely long.

Another way to look at it is that although we have infinitely many terms in the series we are limited to using sinusoidals with only a small subset of possible frequencies, specifically we can only use multiples of the fundamental frequency. Observe that the frequencies are seperated by $$\frac{n}{T}$$, thus by making the period $$T$$, the intervals between subsequent frequencies is becoming smaller. So the idea is to use a all the possible frequencies thus forming a continous range of frequencies.

Since we are integrating over $$x$$, our coefficient is a function of $$n$$ and $$T$$ (we can convince ourselves of that by noticing that if we change either of these variables the coefficient will change as well). So let us define this as a variable $$w_n=\frac{n}{T}$$, for reference and to reiterate that the coefficients are functions that vary with $$n$$ and $$T$$ rather than constants we can rewrite $$(6)$$ as

$$
C(w_n) = \frac{1}{T}\int_{-T/2}^{T/2} f(x) e^{2πi(w_n)x}dx
$$

Take a moment to convince yourselves that we have not changed anything, just renamed the variables to make the explicit connection between the dependent variable $$C$$ and the independent variables $$n$$ and $$T$$. By taking the limit as $$T→∞$$ we get the Fourier transform (again we'll assume the limit exists):

$$
C(w) = \int_{-∞}^{∞} f(x) e^{2πiwx}dx
$$

To derive the inverse Fourier transform, we can plug $$(6)$$ into the complex form of the Fourier series:

$$
f(x) = \sum_{-∞}^∞ C(w_n) e^{2πi(w_n)x} \\[2ex]
= \sum_{-∞}^∞ [\frac{1}{T} \int_{-T/2}^{T/2} f(x) e^{2πi(w_n)x}dx] e^{2πi(w_n)x}
\tag{7}
$$

Lets define a few terms:

$$\Delta{w_n}=\frac{n+1}{T}-\frac{n}{T}=\frac{1}{T} \\[2ex]
\hat{f}(w_n)=\int_{-T/2}^{T/2} f(x) e^{2πi(w_n)x}dx
$$ 

By plugging $$\Delta{w_n}$$ and $$\hat{f}(w_n)$$ into $$(7)$$ we get:

$$
= \sum_{-∞}^∞ \hat{f}(w_n) e^{2πi(w_n)x} \Delta{w_n}
\tag{8}
$$

Recall the definition of the Riemann integral

$$
\lim_{\Delta x_i→0} \sum_{i=1}^n f(x_i)\Delta{ x_i} = \int_{a}^b f(x)dx
$$

Similarly, if take the limit of $$(8)$$ we get the inverse Fourier Transform:

$$
f(x)=\lim_{\Delta w_n→0} \sum_{-∞}^∞ \hat{f}(w_n) e^{2πi(w_n)x} \Delta{w_n} = \int_{-∞}^∞ f(w)e^{2πiwx}dw
$$

At last we have derived the infamous Fourier series and Fourier transform. In the following articles we will further explore their applications.
