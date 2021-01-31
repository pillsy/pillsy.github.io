---
layout: post
title:  "There are lots of primes"
---

Really, "lots" doesn't even cover it, because there are an infinite number
of prime numbers. Like most interesting facts in mathematics, there are 
many ways of proving this. The most familiar, and probably oldest, appears 
in [Euclid's *Elements*][euclid].

It's a very simple proof by contradiction. Start by assuming that there are 
only $ N $ primes, $ p_1, \ldots, p_N $. If you multiply them all together 
and add one, you get

$$ m = p_1 \cdots p_N + 1 $$

None of the $ p_j $s divide $ m $, so either $ m $ itself is prime or 
it has a prime factor $ q \ne p_i $ for all $ i $. Either way, there 
must be a prime that wasn't in our original set, contradicting the 
assumption that there are only a finite number of primes. 

Euclid's proof may be a classic, but it's not my favorite. My favorite is 
more complicated. Complexity is not usually a virtue, but the roundabout 
nature of this proof is, in a word, neat. It depends on two very important
facts, neither of which I'll prove because I'm lazy.

The first fact is that any positive integer $ m $[^names] has a unique 
"prime factorization", which means that

$$ m = p_1^{k_1} \cdots p_n^{k_n} $$

where the $ p_i $s are **distinct** primes and the $ k_i$s are positive 
integers[^fta]. If you allow the $ k_i $s to be zero, the factorization is 
no longer unique. On the other hand, $ n $ itself can be zero, in which case 
$ m = 1 $, because the product of an empty list of things is $ 1 $.[^monoid] 

The second fact is that the harmonic series diverges. The harmonic series is
the sum

$$ \frac{1}{1} + \frac{1}{2} + \frac{1}{3} + \cdots $$

As you sum together more and more terms in the series, the total keeps 
growing without bound. If you pick some number $ x $, there's a number 
$ L $ such that if I sum together $ L $ or more terms, the result will 
be greater than $ x $. It doesn't matter what value you pick for $ x $:
eventually the total will be larger. For even a relatively small 
$ x $, However, you'll need to sum **a lot** of terms. If $ x = 10 $, 
you'll need to sum more than $12\,000$ of them![^terms]

Now, rewrite the denominator for each term in the harmonic series as its 
prime factorization, like so:

$$ \frac{1}{1} + \frac{1}{2^1} + \frac{1}{3^1} + \frac{1}{2^2} + 
   \frac{1}{5^1} + \frac{1}{2^1 3^1} + \cdots $$

Already, it seems like I can pull out powers of $ 1/2 $, turning the 
infinite series into a product of **two** infinite series:

$$ \left(\frac{1}{2^0} + \frac{1}{2^1} + \frac{1}{2^2} + \cdots \right) 
     \left(\frac{1}{1} + \frac{1}{3^1} + \frac {1}{5^1} + \cdots\right) $$

If you aren't convinced, try expanding out only the explicitly listed terms
and see that everything up to $ 1/6 $ is included, along with some 
other terms. 

Now, I'm going to assume, again, that there are only $ N $ primes[^cons], 
$ p_1, \ldots, p_N $. For convenience, I'll assume that they're indexed 
in order of their size, so $ p_1 = 2 $, $ p_2 = 3 $, and so on. By 
repeatedly factoring out powers of $ 1/p_j $ for each of the primes 
$ p_j $, I can write the harmonic series a product of $ N $ infinite 
series.

$$ \left( \frac{1}{2^0} + \frac{1}{2^1} + \frac{1}{2^2} + \cdots \right) 
   \left( \frac{1}{3^0} + \frac{1}{3^1} + \frac{1}{3^2} + \cdots \right) 
   \cdots
   \left( \frac{1}{p_N^0} + \frac{1}{p_N^1} + \frac{1}{p_N^2} + \cdots \right) 
$$

This looks much prettier with product and sum notation, using big 
capital $\Pi$s and $\Sigma$s:[^notation]

$$ \prod_{j = 1}^N \left(\sum_{k = 0}^\infty \frac{1}{p_j^k}\right) $$

Then using the basic fact that $ 1/p_j^k = (1/p_j)^k $, the sums are 
revealed to be geometric series. As long as $ -1 < x < 1 $, 

$$ \sum_{k = 0}^\infty x^k = \frac{1}{1-x} $$

Now the harmonic series is just a simple, finite product![^euler]

$$ \prod_{j = 1}^N \frac{1}{1 - 1/p_j } $$

Of course, if the harmonic series is a product of a finite number of 
finite terms, then it must be finite. Since we know the harmonic series 
diverges, we have another contradiction, again showing that the assumption
that there are a finite number of primes is false. QED, as we say in the 
business.

[^names]: This $ m $ is completely independent from the $ m $ used above. 
    One of the hardest parts about programming is coming up with good names
    for functions and variables; in math this is even harder, since 
    long-standing tradition means sticking to names that are a single 
    letter! In the face of such scarcity, mathematicians recycle 
    aggressively. 

[^fta]: This fact is **so** important that some people call it the 
    [Fundamental Theorem of Arithmetic][fta]!

[^monoid]: This is a general property of [monoids][monoid], where using a 
    monoid operation to fold together an empty list of elements always gives 
    the identity element. 

[^terms]: I found the answer using a trick I may talk about in a future 
    post, but you can also find the answer by brute force. For instance,
    it's a one-liner in Haskell:

    ~~~ haskell
    length . takeWhile (<= 10) . scanl (+) 0 . map (1 /) $ [1..]
    ~~~ 

    If you copy and paste that into GHCi, you should get `12367` as the
    result. This will run instantaneously, but be careful, because as 
    $ x $ gets larger, it'll get very slow very fast.

[^cons]: One interesting consequence of having a finite number of primes 
    is that when you factor a number into primes, you can include **all** 
    the primes, some raised to the zeroth power, and still have a unique 
    way of writing the factorization!
 
[^notation]: This notation is very similar to a `for` loop. In the curly
    brace language of your choice, 

    $$ \sum_{k = 1}^{n} f(k) $$ 

    is equivalent to 

    ~~~ java
    double result = 0.0;

    for (int k = 1; k <= n; ++k) { 
      result += f(k);
    }

    return result;
    ~~~

    In addition to using the same damn one-letter variable names over
    and over agin, no matter how confusing it is, mathematicians also
    have an [annoying habit of indexing from one][index].
 
[^euler]: This is called the ["Euler product"][euler], after Leonhard 
    Euler, who discovered it. I'm pretty sure the second proof in this
    post is also due to Euler. 

[euclid]: http://primes.utm.edu/notes/proofs/infinite/euclids.html

[fta]: http://mathworld.wolfram.com/FundamentalTheoremofArithmetic.html

[monoid]: https://apocalisp.wordpress.com/2010/06/14/on-monoids/

[index]: http://www.cs.utexas.edu/users/EWD/ewd08xx/EWD831.PDF

[euler]: https://en.wikipedia.org/wiki/Riemann_zeta_function#Euler_product_formula
