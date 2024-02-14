+++
title = "Monkey-patching Pandas"
author = ["Josh Friedlander"]
date = 2023-09-12
draft = false
math = true
+++

A common catch for [Pandas](https://pandas.pydata.org/) users is that the default `DataFrame.to_csv` option is `index=True`. Indices are often significant in Pandas, but perhaps just as often a simple range of integers $0..n$ adding no new information. You can see some expressions of annoyance about it in [this thread](https://github.com/pandas-dev/pandas/issues/34576), where Joris Van den Bossche (a Pandas core contributor and GeoPandas maintainer) notes that GeoPandas went with a much smarter default of checking if the index is non-standard and only adding it in this case.

Anyway, for me most of the time when casting to CSV I just want to send it to a colleague who will look at it in Excel or something, so I patched it in my `$HOME/.ipython/startup.py`. The key insight here for me was how to use `partial` with a class method; for this Python 3.4 added `partialmethod`.

```python
from functools import partialmethod
import pandas as pd

pd.DataFrame.to_csv = partialmethod(pd.DataFrame.to_csv, index=False)
```

(If you want this in a regular Python REPL there is also `$HOME/.pythonrc.py`.)
