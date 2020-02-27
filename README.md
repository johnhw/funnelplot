# Title
> summary


# Funnel plot

Provides simple [funnel plots](https://psmu.improvement.nhs.uk/psc-shared-library/measurement-evidence-base/16-funnel-plots-for-comparing-institutional-performance/file) in Python, using Matplotlib. This lets you quickly see whether sub-groups of a population are outliers compared to the full population.

Two methods are provided:

* **parametric funnelplot** which uses a standard distribution to estimate the intervals of the funnel (usually a normal distribution)
* **bootstrap funnelplot** which uses bootstrapped percentiles to estimate the intervals of the funnel 

## Example
Data of test performance for California schools from [`pydataset/Caschool`](https://pypi.org/project/pydataset/).

<img src="imgs\caschool_example.png" width="50%">

## Install

`pip install funnelplot`

## Examples

```python
# load some example data
import pandas as pd
import matplotlib.pyplot as plt
from pydataset import data
fig,ax = plt.subplots(figsize=(4,9))
ax.set_frame_on(False)

# funnel plot
funnel(df=data("Caschool"), x='testscr', group="county")
```

    1.959963984540054
    


![png](docs/images/output_5_1.png)


## Synthetic data example

```python
## Synthetic data
import numpy as np
import random
random.seed(2020)
np.random.seed(2020)
groups = []
p_mean, p_std = 0, 1
for i in range(25):
    n_group = np.random.randint(1, 80)
    g_std =  np.random.uniform(0.1, 4.5) 
    g_mean = np.random.uniform(-1.9, 0.5)
    groups.append(np.random.normal(p_mean + g_mean,
                                   p_std + g_std, 
                                   n_group))
```

```python


ax, fig = plt.subplots(figsize=(9, 9))
funnel_plot(
    groups,
    labels=[random.choice("abcdefg") * 4 for i in range(len(groups))],
    percentage=97.5,
)
```

    1.959963984540054
    


![png](docs/images/output_8_1.png)

