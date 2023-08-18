# SUES-Digit Project - Sankey WebPage

This repository contains the programs and files needed to execute the webpage that display a Sankey Diagram with the energy data of different municipalities.
(16/08/2023) This program functions for Skara and Lidköping.

> 🚧 It is needed to download the whole folder and files have to be in their respectives folders. It is also needed to have Python installed as well as some libraries.🚧

## Documentation
The documentation for the files used cann be found in the [Documentation/](Documentation) directory.
In this pages it is explained how the different code files work.

- [01-Main.md](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/01_Main.md)
    
- [02-SankeyDiagram.md](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/02_SankeyDiagram.md)
    
- [03-DataProcessing.md](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/03_DataProcessing.md)
    
This is to explain the manual dictionaries needed to make the program work properly.

- [04_DictionariesDocumentation.md](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/04_DictionariesDocumentation.md)
    
Here, they are proposed some possible improvements and how to implement them. As well as, possible errors that can appear when executing or implementing new features.

- [05-PossibleImprovements.md](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/05_PossibleImprovements.md)
    
- [06-PossibleErrorsAndSolutions.md](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/06_PossibleErrorsAndSolutions.md)

## Installation
This program is written in Python. A confortable way to execute and edit it is by using Code Editor : "Visual Studio Code".

### This is the official link to download it: (https://code.visualstudio.com/)
And this the official beginner tutorial of 7 min to get used to it. Here, it explains also how to create python files and add python extension (3:25 min): (https://code.visualstudio.com/docs/introvideos/basics) -> In this page, you can also find more explanatory videos, but seeing this first one is enough to start.

(Also, to learn more about Python, we have found that there are quite good tutorials in Linkedin Learning.)

Once "Visual Studio Code" is installed, let's use its terminal to install libraries. Copy and paste these instructions in the Visual Studio Code terminal:

```
pip install dash
```
```
pip install numpy
```
```
pip install pandas
```
```
pip install requests
```
```
pip install dash_bootstrap_components
```

## How to start the app


- Download the project from github in .zip format. Unzip it.

- Open Visual Studio Code.

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/ff8264e85e8b7427397ec1089e9782e9d07af910/Documentation/images/visualStudio.png)

- Open the folder: `Final Folder`

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/ff8264e85e8b7427397ec1089e9782e9d07af910/Documentation/images/OpenFolder.png)

Open the path to the `Executable folder` as shown in the following image:

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/078f5d7bc671c3fdedaac770d2fc455eccf1e787/Documentation/images/OpenFolder2.png)

- To run the code you have to open the file [A_main.py](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/9db065e34b31415f3882853da31df71e24c3be1c/1.%20EXECUTABLE/A_main.py) and press `Run Python File`

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/7786b9b7ecb4ccbda4e74b6f7fab96a29647be5d/Documentation/images/runpythonfile.png)

- `Ctrl+Click` the link as it is shown to open the web interface

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/3320bff8b989841c40aa48432878c611ab2cf790/Documentation/images/runScript.png)

### 🚧IMPORTANT!!! To stop the simulation of the code, type `Ctrl+C` in the Visual Studio Code terminal
