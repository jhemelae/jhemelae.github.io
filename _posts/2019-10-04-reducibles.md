---
layout: post
title: "Patterns made by the reducible quadratic polynomials modulo n"
date: 2019-10-04
---

Take an integer $$n \geq 2$$. Then we can create an interesting pattern as follows: we draw a blue dot on coordinate $$(b,c)$$ if the polynomial $$x^2+bx+c$$ is reducible modulo $$n$$. This pattern repeats itself vertically and horizontally because we're working modulo $$n$$.

In other words, we draw a blue dot on $$(b,c)$$ if we can find natural numbers $$x_1$$ and $$x_2$$ such that $$b-x_1-x_2$$ and $$c-x_1 x_2$$ are both divisible by $$n$$.

This is the result for $$n=5$$:

![reducibles-5-25](/images/reducibles-5-25.png)

And for $$n=7$$ we get:

![reducibles-7-25](/images/reducibles-7-25.png)

In both cases, the pattern is repeated 25 times, and python automatically draws each block in a different color.

Here are the patterns for all numbers $$n$$ starting at $$n=2$$ and ending with $$n=199$$ (with one "block" per pattern). It seems that the prime numbers have the most chaotic patterns...

<div style="display: flex;align-items: center;justify-content: center;flex-wrap: wrap;margin-left: auto;margin-right: auto;width: 80%;">
{% for i in (2..199) %} ![reducibles-{{i}}](/images/reducibles-{{i}}.png) {% endfor %}
</div>
