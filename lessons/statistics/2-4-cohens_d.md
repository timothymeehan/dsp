[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

Question: Are first babies born heavier or lighter than subsequent ones?

Approach: Compute Coehn's d between first and subsequent babies' birth weights

First, import the pandas and numpy, plus Alan Downey's nsfg package. Get the data using AD's function:

```python
import pandas as pd
import numpy as np
import nsfg

preg = nsfg.ReadFemPreg()
```

We can restrict the analysis to live births only:

```python
live_births = preg[preg['outcome'] == 1]
```

Create two groups, one of first order babies, one of higher order babies:

```python
firsts = preg[preg['birthord'] == 1]
others = preg[preg['birthord'] != 1]
```

Now we need a function that computes Cohen's d. Largely following AD's, write one below:

```python
def cohens_d(group1, group2):
    """
    Computes Cohen's distance measure between two groups
    
    Input: two series or dataframes containing features to compare
    
    Returns: float for a series, series for a dataframe
    """
    
    var1, var2 = group1.var(), group2.var()
    n1, n2 = len(group1), len(group2)
    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    
    meandiff = group1.mean() - group2.mean()
    
    d = meandiff/np.sqrt(pooled_var)
    
    return d
```

Input the two groups and get Cohen's d between them:

```python
print(cohens_d(firsts['totalwgt_lb'], others['totalwgt_lb']
```

This gives the value -0.08893641177719079, which means that first babies are lighter than subsequent ones on average by ~-0.09 standard deviations. This is quite small, and, like the difference between pregnancy lengths, is probably nothing.
