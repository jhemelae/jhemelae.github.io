---
layout: post
title: "Patterns made by the reducible quadratic polynomials modulo n"
date: 2019-10-04
---

Take an integer $$n \geq 2$$. Then we can create an interesting pattern as follows: we draw a dot on coordinate $$(b,c)$$ if the polynomial $$x^2+bx+c$$ is reducible modulo $$n$$. This pattern repeats itself vertically and horizontally because we're working modulo $$n$$.

In other words, we draw a dot on $$(b,c)$$ if we can find natural numbers $$x_1$$ and $$x_2$$ such that $$b-x_1-x_2$$ and $$c-x_1 x_2$$ are both divisible by $$n$$.

This is the result for $$n=5$$:

![reducibles-5-25](/images/reducibles-5-25.png)

And for $$n=7$$ we get:

![reducibles-7-25](/images/reducibles-7-25.png)

In both cases, the pattern is repeated 25 times, and Python automatically draws each block in a different color.

Here are the patterns for all numbers $$n$$ starting at $$n=2$$ and ending with $$n=199$$ (with one "block" per pattern). It seems that the prime numbers have the most chaotic patterns... If you want to see the Python code generating the images, you have to keep scrolling.

<div style="display: flex;align-items: center;justify-content: center;flex-wrap: wrap;margin-left: auto;margin-right: auto;width: 100%;">
{% for i in (2..199) %} <figure style="margin-top:0px;margin-bottom:0px;"><img src="/images/reducibles-{{i}}.png" alt="Pattern for n={{i}}" width="144" style="vertical-align: middle;"><figcaption style="line-height:0px;margin-top:-20px;margin-bottom:0px;">$$n={{i}}$$</figcaption></figure> {% endfor %}
</div>

As promised, here is the Python code. I run this inside a [Jupyter notebook](https://jupyter.org/).

~~~ python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
from itertools import product

for p in range(2,200):
    N1=1   # number of times the pattern is repeated horizontally
    N2=1   # number of times the pattern is repeated vertically
    numberofdots = N1*N2*(p*p + p)/2       # estimate (!) of number of dots
    d = 1.1
    s0 = 10000.0/pow(numberofdots,d)       # area of each dot should decrease for larger number of dots
    l = list(range(p))                     # list of numbers modulo p

    b_list = [x_1+x_2  for x_1,x_2 in product(l,l)]        # b-coefficients of reducible polynomials
    c_list = [x_1*x_2  for x_1,x_2 in product(l,l)]        # c-coefficients of reducible polynomials

    # convert to numpy arrays
    b = np.asarray(b_list)
    c = np.asarray(c_list)

    # plot layout
    axes = plt.gca()
    axes.set_aspect('equal','box')
    axes.set_xlim([0,N1*p])
    axes.set_ylim([0,N2*p])
    plt.xticks([0,p])
    plt.yticks([0,p])

    # scatter plotting all dots, each with the correct size
    for i in range(N1+1):
        for j in range(N2+1):
            plt.scatter(p*i + b % p, p*j + c % p, s=s0)
            
    plt.show()
~~~
