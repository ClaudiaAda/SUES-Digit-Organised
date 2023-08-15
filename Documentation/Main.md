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

Once you execute this command your app is now running and you can see you dashboard by the link provided which is your localhost.

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

```
    
- `id`="string",

    The ID of this component, used to identify dash components in callbacks

- `optionHeight`= number (),

    Height of each option

- `maxHeight`= number (),

    Height of the options dropdown

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

#### See the [RangeSlider Components](https://dash.plotly.com/dash-core-components/rangeslider) in the Plotly official documentation for more information.

> How to declare a dropdown component:
```python
dcc.RangeSlider(
    id="slider",
    min=0,
    max=1,
    step=0.05,
    value=[None,None],
),
```
Let's define the attributes of this component, what they do and what input they need.

```
    
- `id`="string",

    The ID of this component, used to identify dash components in callbacks

- `min`= number (),

    Minimum allowed value of the slider

- `max`= number (),

    Maximum allowed value of the slider

- `step`= number (),

    Value by which increments or decrements are made

- `mark`=dict{ 

    - `label`= list["name0","name1","name2",...] (Names of the marks)
    - `style`=  dict{} (layout setting)

    (Marks on the slider. The key determines the position (a number), and the value determines what will show)
}

- `vertical`= (Boolean) (If True, the slider will be vertical)
- `value`= (list of numbers) (The value of the input)

```

This is how the component will look like in the script:

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/aca67e98bdbb90c9c2608cec1eadee7d1a266966/Documentation/images/RangeSlider.png)


### CheckList

#### See the [CheckList Components](https://dash.plotly.com/dash-core-components/checklist) in the Plotly official documentation for more information.

> How to declare a dropdown component:
```python
dcc.Checklist(
    style = {"font-weight": "bold" },
    id='peak_value',
    options=[
        {'label':"peak_hour", 'value': "PeakHourW"},
    ],
),
```
Let's define the attributes of this component, what they do and what input they need.

```

- `id`="string",

    The ID of this component, used to identify dash components in callbacks

- `style`= dict{},

    The style of the container (div)

- `options`=dict{ 

    - `label`= list[string or number] (The option's label)
    - `disabled`=  (boolean) (If True, this option is disabled and cannot be selected)
    - `title`= (string) (The HTML 'title' attribute for the option)
    - `value`=  (string | number | boolean) (The value of the option)

    (Marks on the slider. The key determines the position (a number), and the value determines what will show)
}

- `inline`= (Boolean) (True=horizontal, False=Vertical)
- `value`= (list of strings | numbers | booleans) (The currently selected value)

```
This is how the component will look like in the script:

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/aca67e98bdbb90c9c2608cec1eadee7d1a266966/Documentation/images/CheckItem.png)


### RadioItems

#### See the [RadioItems Components](https://dash.plotly.com/dash-core-components/radioitems) in the Plotly official documentation for more information.

> How to declare a dropdown component:
```python
dcc.RadioItems([                                                    
    {
        "label":
            [
                html.Img(src="/assets/winter.png",height=30),
                html.Span(id="winter", children=" Winter"),
            ],
        "value": "Winter",
    },
    {
        "label":
            [
                html.Img(src="/assets/Sun.png",height=30),
                html.Span(id="summer", children=" Summer"),
            ], 
        "value": "Summer",
    },
    
], 
inline=True, 
labelStyle={ "align-items": "center"},
),
```
Let's define the attributes of this component, what they do and what input they need.

```
- `style`= dict{},

    The style of the container (div)

- `options`=dict{ 

    - `label`= list[string or number] (The option's label)
    - `disabled`=  (boolean) (If True, this option is disabled and cannot be selected)
    - `title`= (string) (The HTML 'title' attribute for the option)
    - `value`=  (string | number | boolean) (The value of the option)

    (Marks on the slider. The key determines the position (a number), and the value determines what will show)
}

- `inline`= (Boolean) (True=horizontal, False=Vertical)
- `value`= (list of strings | numbers | booleans) (The currently selected value)

```
This is how the component will look like in the script:

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/aca67e98bdbb90c9c2608cec1eadee7d1a266966/Documentation/images/RadioItems.png)


### Markdown

#### See the [Markdown Components](https://dash.plotly.com/dash-core-components/markdown) in the Plotly official documentation for more information.

> How to declare a dropdown component:
```python
dcc.Markdown(
    id='slider2_scale3',
    children ="New houses", 
    style = {"textAlign" : "left"}   
),
```
Let's define the attributes of this component, what they do and what input they need.

```

- `id`="string",

    The ID of this component, used to identify dash components in callbacks

- `style`= dict{},

    The style of the container (div)

- `children`= (string | list of strings)

    A string (or array of strings) that are displayed as text.

```


### Graph

#### See the [Graph Components](https://dash.plotly.com/dash-core-components/graph) in the Plotly official documentation for more information.

> How to declare a dropdown component:
```python
dcc.Graph(
    id = "graph",
),
```
Let's define the attributes of this component, what they do and what input they need.

```

- `id`="string",

    The ID of this component, used to identify dash components in callbacks

- `style`= dict{},

    The style of the container (div)

- `hoverData`= (dict)

    Data from latest hover event. Read-only.
- `figure`= (dict)

    Ploty figure object

```
### Others subComponents: They are related to the text and image display

#### html.Label("")

See the [Label Components](https://dash.plotly.com/dash-html-components/label) in the Plotly official documentation for more information.

#### html.P

See the [Paragraph Components](https://dash.plotly.com/dash-html-components/p) in the Plotly official documentation for more information.

#### html.Img

See the [Image Components](https://dash.plotly.com/dash-html-components/img) in the Plotly official documentation for more information.


#### html.H1

See the [Header Components](https://dash.plotly.com/dash-html-components/h1) in the Plotly official documentation for more information.

#### html.Hr

See the [Horizontal Ruler Components](https://dash.plotly.com/dash-html-components/hr) in the Plotly official documentation for more information.


## Style settings

These settings relate to the size of objects and text, their orientation, alignment, font, colour, background, underlining, etc.
These customization parameters are embeded in a whole `html.Div` and align them as you like. Different div parents can have different style settings.
Another way of styling a web page is using a external .css file. You need to create a folder named as `assets` and create a .css file inside it which will be applied to your app. You can name the css file by any name you want. The classname is the place where you apply those  customizations of your dashboard.

> How to declare a style atribute:
```python
style={
    'backgroundColor':'darkslategray',
    'background-size': '100%',
    'color':'lightsteelblue',
    'height':'100px',
    'margin-left':'10px',
    'text-align':'center',
    'width':'40%',
    'display':'inline-block'
},
```
These parameters are pretty self-explanatory and there are many more.
#### In this web page: [Html Style](https://www.w3schools.com/jsref/dom_obj_style.asp), there is more information.


## Callbacks settings 

Callbacks help to make the dashboard a lot more interactive and representative. Input values can be passed by dropdowns, checklists, buttons, etc. and expect an output to be displayed accordingly.

`app.callback()` has 2 parameters: `Output` and `Input`. For the `Output` you have to specify the id for the div where you want your output to be displayed and type of the output. Whereas `Input` specifies id of the component from which input value is to be received and which type of value stores the value that is passed from the dashboard. 
Every callback has a function (`def name(input values)`) that will be executed for the given callback. It should return a children, div o ,figure for graphs, etc.

> The syntax for callback is as follows:
```python
@app.callback(
    Output("unit", "options"),
    Output("wintersummer", "style"),
    Input("peak_value", "value")
)

def unit_menu(value):
    
    if value == ['PeakHourW']:
        options = [
            {'label' : 'kW', 'value' : 'kilo' },
            {'label' : 'MW', 'value' : 'mega' },
            {'label' : 'GW', 'value' : 'giga' }
        ]
        style = {'display':'block'}

        return options, style
    else: 
        options = [
            {'label' : 'kWh', 'value' : 'kilo' },
            {'label' : 'MWh', 'value' : 'mega' },
            {'label' : 'GWh', 'value' : 'giga' }
        ]
        style = {'display':'none'}

        return options, style
```
#### See these pages: [Basic Dash Callbacks](https://dash.plotly.com/basic-callbacks) and [Advanced Callbacks](https://dash.plotly.com/advanced-callbacks) in the Plotly official documentation for more information.
