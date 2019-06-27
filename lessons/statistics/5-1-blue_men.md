[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

Task: Given that height is roughly normally distributed in the population, find the percentage of adult males that fall within the range of required heights to qualify for the blue man group

Approach: Use the cdf of the normal distribution to compute the percentile ranks of the low and high end of the ranges and take the difference

First, we just need to import the stats module from scipy:

```python
import scipy.stats as stats
```

Convert the low and high ends of the range to cm using a simple function:

```python
def in_to_cm(inches):
    return inches * 2.54
    
range_lo = in_to_cm(70)
range_hi = in_to_cm(73)
```

Now, generate a normal distribution with the parameters for male heights and use the cdf method to calculate the difference between the percentile ranks:

```python
dist = stats.norm(loc=178, scale=7.7)

range_pct = (dist.cdf(range_hi) - dist.cdf(range_lo)) * 100

print(range_pct)
```
34.274683763147457
