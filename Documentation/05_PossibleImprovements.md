# Possible Improvements 

In this area, some ideas are left to be developed in depth to improve the project as future ideas.

They are listed bellow:

## Multipages on html

In order to show different diagrams in the future, an interactive web page can be created where you can change pages in a simple way. The idea would be to have a main homepage and associated subpages that are called and selected in some way (with buttons for example).

#### See the video [Multipage Dash Python App](https://www.youtube.com/watch?v=MtSgh6FOL7I&ab_channel=CharmingData) for more information and get and idea of it.


## Server-Mobile App

Right now, access to all the files, images etc. of the project is done locally and therefore you can only see the website locally on the computer where the code is running and where the files are. 

An idea for the future would be to broaden the scope of the project and create an official website and host it. The website could be visited via internet by anyone. 
It could be implemented using the university's servers as a host.

## Summer/Winter Peak Hours Options

Once you have the .csv files with all the peak hour data in all possible scenarios upload them into the "Scenarios" folder. It is important that the name of these files follows the standardisation: 

For constants:
> vensim_data_Constants_`kommun`_ver.csv

For variables year values:
> vensim_data_Scen`scenario`_`kommun`_ver.csv

For variables peakhours:
> vensim_data_Scen`scenario`_PeakHour`winter_summer` _`kommun`_ver.csv

Where:

- `kommun`: Skara|Lidköping
  
- `scenario`: 1|2|3|4|5|6|All
  
- `winter_summer`: W|S

## Styling the sankey

Improve the code of the web display to make it more efficient and less resource-consuming. Improve its aesthetic appearance. 

One idea would be to add images depending on the region you select in the sankey and have them change. This idea would be implemented using `html.img` and `callbacks`. The difficulty lies in finding a suitable image that complies with the size measurements more or less so that it looks good as a background.

### Hovertemplate in the links 
It would be nice to have consistency in the sankey notes. Links and nodes follow the same criteria. the fix is basically to find a list of names that can be represented in the diagram and at the same time show the value of the link and its unit. It is not difficult to fix in the future.

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/e6221335a0c52af26fa76ccd5a5f988d22eefb0e/Documentation/images/hovertemplate.png)

### Show values next to the Sankey 
It would be nice to find a way to show the name of the nodes so that they are more visible in the sankey diagram as shown in the picture.
An idea to implement this would be to put a table with the names next to the figure and make the names of the figure invisible. The table would have the rows and columns invisible as well and only the names would be visible.

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/b6ae4c72dfb91f397cd374c6f40a424f16b3514e/Documentation/images/sankeynames.png)

## Improve in general the code 
There are things that can be done in a more efficient way and in a way that is easier to modify for future datasets and new areas.
Now that there is a better understanding of how the Sankey works and how the data is handled, many things would change to become more automatic.

## .exe documentation

Find a way of displaying the documentation in a proper way out of Github. It would be nice to develop a .exe file or a .doc that it is easy to make interactive, but also that looks as good as in Github looks.
