---
title: "Polynomials"
teaching: 0
exercises: 0
questions:
- "FIXME"
objectives:
- "Learning objective (FIXME)"
keypoints:
- "FIXME"
math: yes
---

## Polynomials

Polynomials in NumPy can be *created*, *manipulated*, and even *fitted*
using the
[convenience classes](https://numpy.org/devdocs/reference/routines.polynomials.classes.html) of the [`numpy.polynomial`](https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial) package, introduced in
NumPy 1.4.

Prior to NumPy 1.4, [`numpy.poly1d`](https://numpy.org/devdocs/reference/generated/numpy.poly1d.html#numpy.poly1d) was the class of choice and it is still available in order to maintain backward compatibility. However, the newer [**polynomial package**](https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial) is more complete and its *convenience classes* provide a more consistent, better-behaved interface for working with polynomial expressions.\
Therefore [`numpy.polynomial`](https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial) is recommended for new coding.



> **Terminology**
> 
> The term *polynomial module* refers to the old API defined in
> `numpy.lib.polynomial`, which includes the
> [`numpy.poly1d`](https://numpy.org/devdocs/reference/generated/numpy.poly1d.html#numpy.poly1d) 
> class and the polynomial functions prefixed with *poly* accessible from the 
> [`numpy`](https://numpy.org/devdocs/reference/index.html#module-numpy)
> namespace (e.g. 
> [`numpy.polyadd`](https://numpy.org/devdocs/reference/generated/numpy.polyadd.html#numpy.polyadd),
> [`numpy.polyval`](https://numpy.org/devdocs/reference/generated/numpy.polyval.html#numpy.polyval), 
> [`numpy.polyfit`](https://numpy.org/devdocs/reference/generated/numpy.polyfit.html#numpy.polyfit), etc.).
> 
> The term *polynomial package* refers to the new API defined in
> [`numpy.polynomial`](https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial), which includes the convenience classes
> for the different kinds of polynomials
> (**numpy.polynomial.Polynomial**,
> **numpy.polynomial.Chebyshev**, etc.).
{: .callout}

## Transitioning from [`numpy.poly1d`](https://numpy.org/devdocs/reference/generated/numpy.poly1d.html#numpy.poly1d) to [`numpy.polynomial`](https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial)

As noted above, the [**poly1d class**(https://numpy.org/devdocs/reference/generated/numpy.poly1d.html#numpy.poly1d)] and associated functions defined in
**numpy.lib.polynomial**, such as [`numpy.polyfit`](https://numpy.org/devdocs/reference/generated/numpy.polyfit.html#numpy.polyfit) and
[`numpy.poly`](https://numpy.org/devdocs/reference/generated/numpy.poly.html#numpy.poly), are considered legacy and should **not** be
used in new code. Since NumPy version 1.4, the
[`numpy.polynomial`](https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial) package is preferred for working with
polynomials.

### Quick Reference

The following table highlights some of the main differences between the
legacy polynomial module and the polynomial package for common tasks.
The [\~numpy.polynomial.polynomial.Polynomial]{.title-ref} class is
imported for brevity:

    from numpy.polynomial import Polynomial

<table class="colwidths-auto table" style="border:1px solid black">
<thead>
<tr class="row-odd">
<th class="head"><p>How to…</p></th>
<th class="head"><p><a href="https://numpy.org/devdocs/reference/generated/numpy.poly1d.html#numpy.poly1d">Legacy (<code class="docutils literal notranslate"><span class="pre">numpy.poly1d</span></code>)</a></p></th>
<th class="head"><p><a href="https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial"><code class="docutils literal notranslate"><span class="pre">numpy.polynomial</span></code></a></p></th>
</tr>
</thead>
<tbody>
<tr class="row-even">
<td><p>Create a polynomial object from coefficients <b>[1]</b></p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">p = np.poly1d([1, 2, 3])</span></code></p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">p = Polynomial([3, 2, 1])</span></code></p></td>
</tr>
<tr class="row-odd">
<td><p>Create a polynomial object from roots</p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">r = np.poly([-1, 1]) p = np.poly1d(r)</span></code></p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">p = Polynomial.fromroots([-1, 1])</span></code></p></td>
</tr>
<tr class="row-even">
<td><p>Fit a polynomial of degree deg to data</p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">np.polyfit(x, y, deg)</span></code></p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">Polynomial.fit(x, y, deg)</span></code></p></td>
</tr>
</tbody>
</table>

<b>\[1\]</b> Note the reversed ordering of the coefficients

### Transition Guide

There are significant differences between `numpy.lib.polynomial` and
[`numpy.polynomial`](https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial). The most significant difference is the
ordering of the coefficients for the polynomial expressions. The various
routines in [`numpy.polynomial`](https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial) all deal with series whose
coefficients go from degree zero upward, which is the *reverse order* of
the poly1d convention. The easy way to remember this is that indices
correspond to degree, i.e., `coef[i]` is the coefficient of the term of
degree **i**.

Though the difference in convention may be confusing, it is
straightforward to convert from the legacy polynomial API to the new.
For example, the following demonstrates how you would convert a
[`numpy.poly1d`](https://numpy.org/devdocs/reference/generated/numpy.poly1d.html#numpy.poly1d) instance representing the expression $x^{2} + 2x + 3$ to a
[Polynomial](https://numpy.org/devdocs/reference/generated/numpy.polynomial.polynomial.Polynomial.html#numpy.polynomial.polynomial.Polynomial) instance
representing the same expression:\

    >>> p1d = np.poly1d([1, 2, 3])
    >>> p = np.polynomial.Polynomial(p1d.coef[::-1])

In addition to the `coef` attribute, polynomials from the polynomial
package also have `domain` and `window` attributes. These attributes are
most relevant when fitting polynomials to data, though it should be
noted that polynomials with different `domain` and `window` attributes
are not considered equal, and can\'t be mixed in arithmetic:

    >>> p1 = np.polynomial.Polynomial([1, 2, 3])
    >>> p1
    Polynomial([1., 2., 3.], domain=[-1,  1], window=[-1,  1], symbol='x')
    >>> p2 = np.polynomial.Polynomial([1, 2, 3], domain=[-2, 2])
    >>> p1 == p2
    False
    >>> p1 + p2
    Traceback (most recent call last):
        ...
    TypeError: Domains differ

See the documentation for the [convenience
classes](routines.polynomials.classes) for further details on the
`domain` and `window` attributes.

Another major difference between the legacy polynomial module and the
polynomial package is polynomial fitting. In the old module, fitting was
done via the [`polyfit`](https://numpy.org/devdocs/reference/generated/numpy.polyfit.html#numpy.polyfit) function. In the polynomial
package, the [`fit`](https://numpy.org/devdocs/reference/generated/numpy.polynomial.polynomial.Polynomial.fit.html#numpy.polynomial.polynomial.Polynomial.fit)
class method is preferred. For example, consider a simple linear fit to
the following data:

~~~
rng = np.random.default_rng() 
x = np.arange(10) 
y = np.arange(10) + rng.standard_normal(10)
~~~
{: .python}

With the legacy polynomial module, a linear fit (i.e. polynomial of
degree 1) could be applied to these data with `[polyfit`](https://numpy.org/devdocs/reference/generated/numpy.polyfit.html#numpy.polyfit):

~~~
np.polyfit(x, y, deg=1)
~~~
{: .python}
~~~
array([0.75901174, 1.23135249])
~~~
{: .output}

With the new polynomial API, the
[`fit`](https://numpy.org/devdocs/reference/generated/numpy.polynomial.polynomial.Polynomial.fit.html#numpy.polynomial.polynomial.Polynomial.fit) class method
is preferred:

~~~
p_fitted = np.polynomial.Polynomial.fit(x, y, deg=1) 
p_fitted
~~~
{: .python}
~~~
Polynomial([4.64690534, 3.41555285], domain=[0., 9.], window=[-1.,  1.], symbol='x')
~~~
{: .output}

Note that the coefficients are given *in the scaled domain* defined by
the linear mapping between the `window` and `domain`.
[`convert`](https://numpy.org/devdocs/reference/generated/numpy.polynomial.polynomial.Polynomial.convert.html#numpy.polynomial.polynomial.Polynomial.convert) can be
used to get the coefficients in the unscaled data domain.

~~~
p_fitted.convert()
~~~
{: .python}
~~~
Polynomial([1.23135249, 0.75901174], domain=[-1.,  1.], window=[-1.,  1.], symbol='x')
~~~
{: .output}

## Documentation for the [`polynomial`](https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial) Package

In addition to standard power series polynomials, the polynomial package
provides several additional kinds of polynomials including Chebyshev,
Hermite (two subtypes), Laguerre, and Legendre polynomials. Each of
these has an associated **convenience class** available from the
[`numpy.polynomial`](https://numpy.org/devdocs/reference/routines.polynomials.package.html#module-numpy.polynomial) namespace that provides a consistent
interface for working with polynomials regardless of their type.

[Using the Convenience Classes](https://numpy.org/devdocs/reference/routines.polynomials.classes.html)

Documentation pertaining to specific functions defined for each kind of
polynomial individually can be found in the corresponding module
documentation:

[Power Series (`numpy.polynomial.polynomial`)](https://numpy.org/devdocs/reference/routines.polynomials.polynomial.html)
[Chebyshev Series (`numpy.polynomial.chebyshev`)](https://numpy.org/devdocs/reference/routines.polynomials.chebyshev.html)
[Hermite Series, “Physicists” (`numpy.polynomial.hermite`)](https://numpy.org/devdocs/reference/routines.polynomials.hermite.html)
[HermiteE Series, “Probabilists” (`numpy.polynomial.hermite_e`)](https://numpy.org/devdocs/reference/routines.polynomials.hermite_e.html)
[Laguerre Series (`numpy.polynomial.laguerre`)](https://numpy.org/devdocs/reference/routines.polynomials.laguerre.html)
[Legendre Series (`numpy.polynomial.legendre`)](https://numpy.org/devdocs/reference/routines.polynomials.legendre.html)
[Polyutils](https://numpy.org/devdocs/reference/routines.polynomials.polyutils.html)

## Documentation for Legacy Polynomials

[Poly1d](https://numpy.org/devdocs/reference/routines.polynomials.poly1d.html)
* [Basics](https://numpy.org/devdocs/reference/routines.polynomials.poly1d.html#basics)
* [Fitting](https://numpy.org/devdocs/reference/routines.polynomials.poly1d.html#fitting)
* [Calculus](https://numpy.org/devdocs/reference/routines.polynomials.poly1d.html#calculus)
* [Arithmetic](https://numpy.org/devdocs/reference/routines.polynomials.poly1d.html#arithmetic)
* [Warnings](https://numpy.org/devdocs/reference/routines.polynomials.poly1d.html#warnings)
