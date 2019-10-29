---
layout: post
title: "Patterns made by the reducible quadratic polynomials modulo n"
date: 2019-10-04
---

Take a natural number $$n \geq 2$$. Then we can create an interesting pattern as follows: we draw a dot with coordinates $$(b,c)$$ if the polynomial $$x^2+bx+c$$ is reducible modulo $$n$$. In other words, we draw a dot on $$(b,c)$$ if we can find natural numbers $$x_1$$ and $$x_2$$ such that $$b-x_1-x_2$$ and $$c-x_1 x_2$$ are both divisible by $$n$$. This pattern repeats itself vertically and horizontally.

This is the result for $$n=5$$:

![reducibles-5-25](/images/reducibles-5-25.png)

And for $$n=7$$ we get:

![reducibles-7-25](/images/reducibles-7-25.png)

In both cases, the pattern is repeated 25 times, and Python automatically draws each block in a different color (for the code, scroll down to the end of the post).

Here are the patterns for all numbers $$n$$ starting at $$n=2$$ and ending with $$n=199$$ (with one "block" per pattern). It seems that the prime numbers have the most chaotic patterns...

<div style="display: flex;align-items: center;justify-content: center;flex-wrap: wrap;margin-left: auto;margin-right: auto;width: 100%;">
{% for i in (2..199) %} <figure style="margin-top:0px;margin-bottom:0px;"><img src="/images/reducibles-{{i}}.png" alt="Pattern for n={{i}}" width="144" style="vertical-align: middle;"><figcaption style="line-height:0px;margin-top:-20px;margin-bottom:0px;">$$n={{i}}$$</figcaption></figure> {% endfor %}
</div>

And here is the Python code. I run this inside a [Jupyter notebook](https://jupyter.org/).

~~~ python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
from itertools import product

for n in range(2,200):
    N1=1   # number of times the pattern is repeated horizontally
    N2=1   # number of times the pattern is repeated vertically
    numberofdots = N1*N2*(n*n + n)/2       # estimate (!) of number of dots
    d = 1.1
    s0 = 10000.0/pow(numberofdots,d)       # area of each dot should decrease for larger number of dots
    l = list(range(n))                     # list of numbers modulo p

    b_list = [x_1+x_2  for x_1,x_2 in product(l,l)]        # b-coefficients of reducible polynomials
    c_list = [x_1*x_2  for x_1,x_2 in product(l,l)]        # c-coefficients of reducible polynomials

    # convert to numpy arrays
    b = np.asarray(b_list)
    c = np.asarray(c_list)

    # plot layout
    axes = plt.gca()
    axes.set_aspect('equal','box')
    axes.set_xlim([0,N1*n])
    axes.set_ylim([0,N2*n])
    plt.xticks([0,n])
    plt.yticks([0,n])

    # scatter plotting all dots, each with the correct size
    for i in range(N1+1):
        for j in range(N2+1):
            plt.scatter(n*i + b % n, n*j + c % n, s=s0)
            
    plt.show()
~~~

To estimate the number of dots in each "block" of the pattern, I use the formula $$(n^2+n)/2$$. This is the exact number of dots if $$n$$ is a prime number, but an overestimate otherwise. As a result, the patterns for prime numbers are more "dense".

The number of dots per block for the first few patterns are 3,6,8,15,18 and 28 (you can count them in the images above). So we search for "3,6,8,15,18,28" in [The On-Line Encyclopedia of Integer Sequences (OEIS)](https://oeis.org). The sequence that we need is [Sequence A261928](https://oeis.org/A261928). We could use this to "repair" the estimate in the code, but I don't think that would make the pictures more interesting.