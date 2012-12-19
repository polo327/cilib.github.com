---
layout: post
title: "RNG Changes: A single stream"
date: 2012-12-19 11:46
comments: true
categories: 
---
Previously, CIlib handled random number generation by creating a new stream of 
random numbers for each RandomProvider that was created. This made it very 
difficult (read: impossible) to reproduce the results of simulations.

The new changes that were merged recently fixes this by using one RNG per sample. 
This post will explain how to use the new system.

<!-- more -->

- The random values are retrieved using static methods in the 
    `net.sourceforge.cilib.math.random.generator.Rand` class.
- If you just need a uniform double use `Rand.nextDouble()` (e.g. for probabilities)
- For other types (boolean, int, long, etc.) use the appropriate `nextX()` methods.
- If your code can use different distributions use the `ProbabilityDistribution`
    classes in the `math.random` package. They use the Rand class internally.
- If you need to set the seed for testing your code use `Rand.setSeed(seed)`.
    You should not set the seed anywhere else in the code.
- Setting the seed for simulations is done in the XML. Look at the
    `simulator/xml/seeder.xml` example file, it shows how to save and set the seed.

Hopefully these changes make using the RNG easier. As usual, if there are any problems
please report them on the issue tracker on github or contact us using IRC or the
mailing list.

