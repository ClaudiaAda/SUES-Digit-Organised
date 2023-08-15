# Main 

In this file the visualisation of the Sanky diagram and the graphical interface of the web page is done. It is the main file from which other files and functions are called. 
Dash and Plotly libraries are used for building a analytical web application with an interactive dashboard in Python.

## Layout Settings

The web page is divided in sections using `dbc.Col()` and `dbc.Row`. In this way a grid system for dividing the screen is created. The grid system divides the screen into 12 columns that can be adjusted (`'weight': '100vw'`). Inside those subsections, there are components split by divisions by using `html.Div`. 
There are two main sections: the upper part where the components are to choose the settings and the bottom part where the graphic is.

#### See the web divisions in the picture below: 

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/dc53b8f1cefbc940fb2611fcc3a23edf835d9a92/Documentation/images/divisions.png)

First of all, the app has to be created:
> How to declare an app:
```python
app = Dash(__name__, external_stylesheets=[dbc.themes.SPACELAB])
```

How to run the script in the terminal after running the code:

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/3320bff8b989841c40aa48432878c611ab2cf790/Documentation/images/runScript.png)


## Component Settings
#### See the [Dash Core Components](https://dash.plotly.com/dash-core-components) in the Plotly official documentation for more information.

### Dropdown

#### See the [Dropdown Components](https://dash.plotly.com/dash-core-components/dropdown) in the Plotly official documentation for more information.

> How to declare a dropdown component:
```python
dcc.Dropdown(
    id = "years",
    optionHeight = 20,
    maxHeight = 500,
    options = [
        {'label' : '2023', 'value' : '0' },
        {'label' : '2024', 'value' : '1' },   
        {'label' : '2025', 'value' : '2' },
        {'label' : '2026', 'value' : '3' },
        {'label' : '2027', 'value' : '4' },
        {'label' : '2028', 'value' : '5' },
        {'label' : '2029', 'value' : '6' },
        {'label' : '2030', 'value' : '7' },
        {'label' : '2031', 'value' : '8' },
        {'label' : '2032', 'value' : '9' },
        {'label' : '2033', 'value' : '10'},
    ],
    placeholder = 'Select a year...',
),
```

Let's define the attributes of this component, what they do and what input they need.

```python
    
- `id`="string",

    The ID of this component, used to identify dash components in callbacks

- `optionHeight`= number (),

    Height of each option

- `maxHeight`= number (),

    Height of the options dropdown.

- `options`=list[

    - `label`= list["name0","name1","name2",...] (Names of the options)
    - `value`= (string | number | boolean) (The value of the option)
]
- `placeholder`= "string"
- `value`= (string | number | boolean) (The value of the input)

```

This is how the component will look like in the script:

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/aca67e98bdbb90c9c2608cec1eadee7d1a266966/Documentation/images/dropdown.png)



### RangeSlider

> How to declare a dropdown component:
```python

),
```

This is how the component will look like in the script:


![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/aca67e98bdbb90c9c2608cec1eadee7d1a266966/Documentation/images/RangeSlider.png)


### CheckList

> How to declare a dropdown component:
```python

),
```
This is how the component will look like in the script:

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/aca67e98bdbb90c9c2608cec1eadee7d1a266966/Documentation/images/CheckItem.png)


### RadioItems

> How to declare a dropdown component:
```python

),
```
This is how the component will look like in the script:

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/aca67e98bdbb90c9c2608cec1eadee7d1a266966/Documentation/images/RadioItems.png)


### Markdown

> How to declare a dropdown component:
```python

),
```

### Graph

> How to declare a dropdown component:
```python

),
```
### Others subComponents
html.Label("")
html.P
html.Img
html.Img
html.H1


## Style settings
## Callbacks settings 

