---
layout: post
title:  "Proving the Infinitude of Primes"
---

There are many ways to prove that there are an infinite number of prime 
numbers. The most familiar, and probably oldest, appears in Euclid. and 
is a very simple proof by contradiction. Start by assuming that there are 
a $ N $ primes, $ p_1, \ldots, p_N $. Then multiply them all together and 
add one, so

$$ m = p_1 \cdots p_N + 1 $$

Then none of $ p_j $s divide $ m $, so either $ m $ itself is prime or 
it has a prime factor $ q \ne p_i $ for all $ i $. 

This is not the proof I want to talk about. The proof I have in mind is
much more complicated. This is not usually a virtue, but the roundabout 
nature of this proof is, in a word, neat. It depends on two very important
facts, neither of which I'll prove because I'm lazy.

The first is that any positive integer $ m $ has a unique "prime 
factorization".
