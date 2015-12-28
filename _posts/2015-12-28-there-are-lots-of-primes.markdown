---
layout: post
title:  "There are lots of primes"
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

The first is that any positive integer $ m > 1 $ has a unique "prime 
factorization". This means that we can write 

$$ m = p_1^{k_1} \cdots p_n^{k_n} $$

where the $ p_i $s are *distinct* primes and the $ k_i$s are positive 
integers. If you allow the $ k_i $s to be zero, the factorization is no
longer unique. On the other hand, $ n $ itself can be zero, in which case 
$ m = 1 $, because the product of an empty set of things is $ 1 $, just 
like the sum of an empty set of things is $ 0 $. 
