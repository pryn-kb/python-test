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
---

## Polynomials

Polynomials in NumPy can be *created*, *manipulated*, and even *fitted*
using the
`convenience classes <routines.polynomials.classes>`{.interpreted-text
role="doc"} of the [numpy.polynomial]{.title-ref} package, introduced in
NumPy 1.4.

Prior to NumPy 1.4, [numpy.poly1d]{.title-ref} was the class of choice
and it is still available in order to maintain backward compatibility.
However, the newer [polynomial package \<numpy.polynomial\>]{.title-ref}
is more complete and its [convenience classes
\<routines.polynomials.classes\>]{.title-ref} provide a more consistent,
better-behaved interface for working with polynomial expressions.
Therefore `numpy.polynomial`{.interpreted-text role="mod"} is
recommended for new coding.

::: note
::: title
Note
:::

**Terminology**

The term *polynomial module* refers to the old API defined in
[numpy.lib.polynomial]{.title-ref}, which includes the
`numpy.poly1d`{.interpreted-text role="class"} class and the polynomial
functions prefixed with *poly* accessible from the [numpy]{.title-ref}
namespace (e.g. [numpy.polyadd]{.title-ref},
[numpy.polyval]{.title-ref}, [numpy.polyfit]{.title-ref}, etc.).

The term *polynomial package* refers to the new API defined in
[numpy.polynomial]{.title-ref}, which includes the convenience classes
for the different kinds of polynomials
([numpy.polynomial.Polynomial]{.title-ref},
[numpy.polynomial.Chebyshev]{.title-ref}, etc.).
:::

## Transitioning from [numpy.poly1d]{.title-ref} to [numpy.polynomial]{.title-ref}

As noted above, the `poly1d class <numpy.poly1d>`{.interpreted-text
role="class"} and associated functions defined in
`numpy.lib.polynomial`, such as [numpy.polyfit]{.title-ref} and
[numpy.poly]{.title-ref}, are considered legacy and should **not** be
used in new code. Since NumPy version 1.4, the
[numpy.polynomial]{.title-ref} package is preferred for working with
polynomials.

### Quick Reference

The following table highlights some of the main differences between the
legacy polynomial module and the polynomial package for common tasks.
The [\~numpy.polynomial.polynomial.Polynomial]{.title-ref} class is
imported for brevity:

    from numpy.polynomial import Polynomial

+-----------------+----------------------+-----------------------------+
| > **How         | Legacy               | [nu                         |
| > to\...**      | ([numpy.             | mpy.polynomial]{.title-ref} |
|                 | poly1d]{.title-ref}) |                             |
+-----------------+----------------------+-----------------------------+
| Create a        | `p = n               | `p = Polynomial([3, 2, 1])` |
| polynomial      | p.poly1d([1, 2, 3])` |                             |
| object from     |                      |                             |
| c               |                      |                             |
| oefficients[^1] |                      |                             |
+-----------------+----------------------+-----------------------------+
| Create a        | `r                   | `p = Pol                    |
| polynomial      |  = np.poly([-1, 1])` | ynomial.fromroots([-1, 1])` |
| object from     | `p = np.poly1d(r)`   |                             |
| roots           |                      |                             |
+-----------------+----------------------+-----------------------------+
| Fit a           | `np                  | `Polynomial.fit(x, y, deg)` |
| polynomial of   | .polyfit(x, y, deg)` |                             |
| degree `deg` to |                      |                             |
| data            |                      |                             |
+-----------------+----------------------+-----------------------------+

### Transition Guide

There are significant differences between `numpy.lib.polynomial` and
[numpy.polynomial]{.title-ref}. The most significant difference is the
ordering of the coefficients for the polynomial expressions. The various
routines in [numpy.polynomial]{.title-ref} all deal with series whose
coefficients go from degree zero upward, which is the *reverse order* of
the poly1d convention. The easy way to remember this is that indices
correspond to degree, i.e., `coef[i]` is the coefficient of the term of
degree *i*.

Though the difference in convention may be confusing, it is
straightforward to convert from the legacy polynomial API to the new.
For example, the following demonstrates how you would convert a
[numpy.poly1d]{.title-ref} instance representing the expression
$x^{2} + 2x + 3$ to a
[\~numpy.polynomial.polynomial.Polynomial]{.title-ref} instance
representing the same expression:

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
done via the [\~numpy.polyfit]{.title-ref} function. In the polynomial
package, the [\~numpy.polynomial.polynomial.Polynomial.fit]{.title-ref}
class method is preferred. For example, consider a simple linear fit to
the following data:

::: ipython
python

rng = np.random.default_rng() x = np.arange(10) y = np.arange(10) +
rng.standard_normal(10)
:::

With the legacy polynomial module, a linear fit (i.e. polynomial of
degree 1) could be applied to these data with \`\~numpy.polyfit\`:

::: ipython
python

np.polyfit(x, y, deg=1)
:::

With the new polynomial API, the
[\~numpy.polynomial.polynomial.Polynomial.fit]{.title-ref} class method
is preferred:

::: ipython
python

p_fitted = np.polynomial.Polynomial.fit(x, y, deg=1) p_fitted
:::

Note that the coefficients are given *in the scaled domain* defined by
the linear mapping between the `window` and `domain`.
[\~numpy.polynomial.polynomial.Polynomial.convert]{.title-ref} can be
used to get the coefficients in the unscaled data domain.

::: ipython
python

p_fitted.convert()
:::

## Documentation for the [\~numpy.polynomial]{.title-ref} Package

In addition to standard power series polynomials, the polynomial package
provides several additional kinds of polynomials including Chebyshev,
Hermite (two subtypes), Laguerre, and Legendre polynomials. Each of
these has an associated [convenience class
\<routines.polynomials.classes\>]{.title-ref} available from the
[numpy.polynomial]{.title-ref} namespace that provides a consistent
interface for working with polynomials regardless of their type.

::: {.toctree maxdepth="1"}
routines.polynomials.classes
:::

Documentation pertaining to specific functions defined for each kind of
polynomial individually can be found in the corresponding module
documentation:

::: {.toctree maxdepth="1"}
routines.polynomials.polynomial routines.polynomials.chebyshev
routines.polynomials.hermite routines.polynomials.hermite_e
routines.polynomials.laguerre routines.polynomials.legendre
routines.polynomials.polyutils
:::

## Documentation for Legacy Polynomials

::: {.toctree maxdepth="2"}
routines.polynomials.poly1d
:::

[^1]: Note the reversed ordering of the coefficients
