# SANKEY DIAGRAM
#### See the [Sankey Diagram in Python](https://plotly.com/python/sankey-diagram/) in the Plotly official documentation for more information.

This file basically takes the previous treated data and assigns it to each parameter of Sankey's function. 

First of all, libraries are imported. Then, we declare a function:
> How to declare a function:
```python
def function_name(parameters)
    content
    return value
```
Inside this function, we create the main figure with function `go.Figure` with the required data. Then `fig.update_layout()` and `fig.update_trace` are used to add features so it is better-looking but that are not essential.

```python
import plotly.graph_objects as go
import pandas as pd

def build_sankey(scen_data,actual_unit):
    fig = go.Figure(data=[go.Sankey(

    )])

    fig.update_layout(

    )

    fig.update_traces(

    )
    return fig
```
