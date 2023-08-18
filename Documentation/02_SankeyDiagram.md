# SANKEY DIAGRAM
#### See the [Sankey Diagram in Python](https://plotly.com/python/sankey-diagram/) in the Plotly official documentation for more information.

This file basically takes the previous treated data in [B_data_processing](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/1.%20EXECUTABLE/B_data_processing.py) and assigns it to each parameter of Sankey's function. 

## Overview

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
    import plotly.graph_objects as go
import pandas as pd


def build_sankey(scen_data,actual_unit):
    # Code to display the Sankey Diagram, it fils the inputs with 
    # the scenario dictionary : scen_data
    fig = go.Figure(data=[go.Sankey(
        arrangement = 'freeform',
        valuesuffix = " "+ actual_unit,
        valueformat = ".2f",
        # Define nodes
        node = dict(
            thickness = 15,
            line = dict(color = "black", width = 0.01),
            label =  scen_data["node"]['label'],
            color =  scen_data["node"]['color'],
            x = scen_data["node"]["x"],
            y = scen_data["node"]["y"],
            pad = 30,
            customdata= scen_data["node"]["percentage"],
            hovertemplate='<b>%{label}</b><br>'+'%{value} <br>'+'%{customdata}'+'<extra></extra>'
        ),
        # Add links
        link = dict(
            arrowlen = 30,
            source =  scen_data["link"]['source'],
            target =  scen_data["link"]['target'],
            color =  scen_data["link"]['color'],
            value = scen_data["link"]['value'],
        )
    )])
 
    fig.update_layout(
        #width = 500, #These 2 parameters determine the size of the graphic
        height = 800,
    )

    fig.update_traces(
        hoverlabel_namelength = -1
    )
    return fig
```
## go.Figure attributes
Let's define the attributes of this function, what they do and what input they need.
```python
fig = go.Figure(data=[go.Sankey(
        arrangement = 'freeform',
        valuesuffix = " "+ actual_unit,
        valueformat = ".2f",
        # Define nodes
        node = dict(
            thickness = 15,
            line = dict(color = "black", width = 0.01),
            label =  scen_data["node"]['label'],
            color =  scen_data["node"]['color'],
            x = scen_data["node"]["x"],
            y = scen_data["node"]["y"],
            pad = 30,
            customdata= scen_data["node"]["percentage"],
            hovertemplate='<b>%{label}</b><br>'+'%{value} <br>'+'%{customdata}'+'<extra></extra>'
        ),
        # Add links
        link = dict(
            arrowlen = 30,
            source =  scen_data["link"]['source'],
            target =  scen_data["link"]['target'],
            color =  scen_data["link"]['color'],
            value = scen_data["link"]['value'],
        )
    )])

```
    
- `arrangement`="snap|freeform|perpendicular|fixed"

    Define how the arrows can be moved around the graphic.

- `valuesuffix`="string"

    Text that appears next to the values of the tags when you mouse over the node or link.

- `valueformat`="special code"

    How it is display the value of the node/link, there are different codes. In this case, ".2f", it is that they are always show with two decimals. To know more definitions this document can be useful [d3-format](https://github.com/d3/d3-format/blob/v1.4.5/README.md#locale_format).

- `node`=dict(
    - `thickness`= number (),

    - `line`= dict(color="colour", width=number) (Bordering line of the nodes),

    - `label`= list["name0","name1","name2",...] (Names of the nodes)

    - `color`= list["rgba(x,y,z,a)","rgba(x,y,z,a)",..] (Colour of each node)

    - `x` and `y` = list[number0,number1,..] (Position of x and y axis, number must be between [0.001,1], NOT 0 that value is not displayed)

    - `pad`= number (Distance between nodes, it does not function for all the nodes, do not know why)

    - `customdata`= list[] (Additional data)

    - `hovertemplate`= special code (Text display when mouse over)
)
    Define the nodes (names displayed) of the Sankey. Lists have to be consistent, the elements of each list are connected because of their position.

- `link`=dict(
    - `arrowlen`= number (Width of the arrow,the final part of the link),

    - `source`= list[number_position(0),...]

    - `target`= list[number_position(0),...] 

    Source and target has de connections between the nodes specified previously source[0] will have a link with target[0], as well as source[n] with target[n]... To make correctly these connections we have to be aware of the position of the energy in the label parameter in node.

    - `color`= list["rgba(x,y,z,a)","rgba(x,y,z,a)",..] (Colour of each link)

    - `value`= number (Value of the connection)
)
    Define the links (connections between the nodes) of the Sankey. Lists have to be consistent, the elements of each list are connected because of their position.

## fig.update
Two functions have been used to implement more features. Only a few have been used, if it is desired to incorporate more see [Update Layout](https://plotly.com/python/reference/layout/) or [Sankey traces](https://plotly.com/python/reference/sankey/)

#### fig.update_layout
```python
    fig.update_layout(
        #width = 500, #These 2 parameters determine the size of the graphic
        height = 800,
    )
```
- `width` and `height` = number

They define the size of the figure

#### fig.update_traces
```python
    fig.update_traces(
        hoverlabel_namelength = -1
    )
```
- `hoverlabel_namelength` = number (Name of characters that are display in the message that appears when mouse over// -1 displays all characters)
