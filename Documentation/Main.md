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
## Style settings
## Callbacks settings 

