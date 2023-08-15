# DATA PROCESSING - [B_data_processing]()
Most complex file, it is were data (excels files) from vensim are treated along manual dictionaries to create dictionary "scen_data" so this data matches [Sankey function](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/SankeyDiagram.md).

### Libraries
Libraries used are:
```python
import json
import pandas as pd
import numpy as np
from functools import reduce
```

## FUNCTION
### Declaration
This function has to receive the excel file from vensim and different parameters chosen in the web page, this inputs are obtained from [main file](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/SankeyDiagram.md).

As result of the function, it will sent "scen_data" and the values of the sum of energies from the production and usage.
```python
def build_scen_data(scen_file, year, scenario,value_slider,value_slider2,v_s3,v_s31,v_s4,v_s41,v_s5,v_s6, unit, kommun, peak_hour, language):
    ...
return (scen_data, s_e_production, s_e_usage)
```

As this function it is very large, let's split in different sections: load and treat data dictionaries, obtain row's position to take the correct value, declaration of node's data, declaration of link's data.

### Load and treat data dictionaries
- 1º loaded dictionary is [All_Labels_Dictionary](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/1.%20EXECUTABLE/D_All_Labels_Dictionary.json) to know more about how the dictionaries are organised and how to add new information see [Manual_Dictionary_Documentation]().

This dictionary is a .json file so is easily loaded with this 2 lines in [info_data].
```python
with open("Latest Folder/D_All_Labels_Dictionary.json") as dictionary:
        info_data = json.load(dictionary)
```

- 2º loaded is a excel file that only contains the names of the energy types, along with the translations in Swedish and corrected English.

This file it is treated to store the energy types' names as the rows of the dataframe, so later we can use this value to find the translation. Translator is the dictionary that stores this data.

 - `pd.read_csv`(""): Store the csv from the path indicated

 - `pd.DataFrame`(data, columns, index): Create a dataframe (table with the information attached)

```python
translator_dictionary = pd.read_csv("Latest Folder\libreria.csv")
rows = list(translator_dictionary["NAMES"])
data1 = list(translator_dictionary["EN"])  
translator = pd.DataFrame(data1, columns = ["EN"], index=rows)
translator["SV"] = list(translator_dictionary["SV"]) 
```

- 3º loaded is the vensim's excel file with the data from the constant variables. Relative path can be written mixing text and declared variables. In this case, it is used the value from the variables from [main file]() to access to the desired file.

Then, in [constant_variables] and [scen_variables] it is stored the names of their respectives energies so later their values are searched in the correct excel file. 
```python
constant_file = pd.read_csv("Latest Folder\Scenarios/vensim_data_Constants_" + kommun + "_ver.csv")
constant_variables = list(constant_file.head(0))
```

- 4º is the declaration for scen_data, the data that is wanted to be exported for [Sankey Diagram](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/SankeyDiagram.md). It has all the attributes needed to create a Sankey.
```python
 scen_data = {"node": { "label":[], "color":[], "x": [], "y": [], "percentage": []},         
                "link": { "source":[], "target":[], "value":[], "color":[]},
                }
```
- 5º declaration of a dictionary to associate a number to each energy type used
```python
node_positions = {}
i = 0 # Total number of nodes
```

- 6º List used to save the y-axis value of the previous energy type to declare correctly his. The first value y[0] is not used, but it is preferred to leave it that way, so the list can be accessed easier.
```python
y = [0,0.01,0.01,0.01] 
```

### Obtain row's position to take correct values
Excel files given store a lot of different values for each energy type, selecting the correct one depends on the parameters chosen. The parameters that determine the correct row are the value(s) of the slider(s).

```python
    columns_names=list(scen_variables)
    column1 = columns_names[1]
 
    scen_file[column1] = pd.Series([round(val,2) for val in scen_file[column1]])
    num_row = [0]
    
    if(scenario=="All"): 
        print("Finishing programming")
        column2=columns_names[2]
        column3=columns_names[3]
        column31=columns_names[4]
        column4=columns_names[5]
        column41=columns_names[6]
        column5=columns_names[7]
        column6=columns_names[8]

        cond1 = np.where(scen_file[column1] == value_slider)
        cond2 = np.where(scen_file[column2] == value_slider2)
        cond3 = np.where(scen_file[column3] == v_s3)
        cond31 = np.where(scen_file[column31] == v_s31)
        cond4 = np.where(scen_file[column4] == v_s4)
        cond41 = np.where(scen_file[column41] == v_s41)
        cond5 = np.where(scen_file[column5] == v_s5)
        cond6 = np.where(scen_file[column6] == v_s6)

        cond1 = cond1[0].tolist()
        cond2 = cond2[0].tolist()
        cond3 = cond3[0].tolist()
        cond31 = cond31[0].tolist()
        cond4 = cond4[0].tolist()
        cond41 = cond41[0].tolist()
        cond5 = cond5[0].tolist()
        cond6 = cond6[0].tolist()
        num_row = list(set(cond1) & set(cond2) & set(cond3) & set(cond31) & set(cond4) & set(cond41) & set(cond5) & set(cond6))

    elif(scenario=="3" or scenario=="4"):
        column2=columns_names[2]
        scen_file[column2] = pd.Series([round(val,2) for val in scen_file[column2]])

        cond1 = np.where(scen_file[column1] == value_slider)
        cond2 = np.where(scen_file[column2] == value_slider2) 

        cond1 = cond1[0].tolist()
        cond2 = cond2[0].tolist()
        num_row = list(set(cond1) & set(cond2))
                                    
    else:
        n_row = np.where(scen_file[column1] == value_slider)
        num_row = num_row[0].tolist()
```

The first columns of the scen_file store the values of the sliders. In first place, it is stored the names of these columns, as many names as sliders has this simulation.

```python
columns_names=list(scen_variables)
column1 = columns_names[1]
```

Sometimes, the values of the slider that are store in the excel file (scen_file) has to many decimals, so they don't coincide with the values stored from the web page's sliders. To be able to compare them, the values from that column of the excel file are rounded

```python
scen_file[column1] = pd.Series([round(val,2) for val in scen_file[column1]])
```

Then, with `np.where(column == value)` it is searched in which row is stored the value selected for that slider. The value given using this function is a bit weird, so we update the variable by converting the value in a list. `cond[0].tolist()`.

```python
cond1 = np.where(scen_file[column1] == value_slider)
cond1 = cond1[0].tolist()
```

If there is only one slider, the number is already the number of the row needed[num_row]. But, if there are more than 1 slider then the conditions will be a list with more than 1 number, these conditions are compare `&` and a common number is obtained. (The use of list and set is to modify value types and be able to use some functions.)

```python
num_row = list(set(cond1) & set(cond2))
```

### Declaration of node's data
In this loop, all energy types declared in [All_Labels_Dictionary] are read. If they appear in the variable or constant file, and if their value is not cero, their name will be stored along a number in node_positions. 

> There is a special case with electric energy export because in some cases its value can be negative, so it has to change its name and properties.

```python
    for label in list(info_data.keys()):

        if info_data[label]["target"] != "link":
            if (("T0 " + label) in scen_variables) or label in constant_variables:
                
                if ("T0 " + label) in scen_variables:
                        node_value = (scen_file["T" + str(year) + " " + label][num_row[0]])
                elif label in constant_variables:
                        node_value = (constant_file[label][0])

                if node_value != 0:
                    if node_value > 0:
                        node_positions[label] = i
                        label2 = label

                    elif node_value < 0: 
                        node_positions["electric energy export"] = i     
                        node_value = -node_value
                        label2 = "electric energy export"
```
Next, it is declared the data necessary for the Sankey of this variables. This data is stored in scen_data. To add information to the dictionary it is used the function `.append()`
```python
    dictionary["pos1"]["pos2"]["..."].append(value)
```
First, it is saved the name that will appear in their nodes (Swedish or English). Then, its color.
```python
                    if language == "SV":
                        scen_data["node"]["label"].append(translator["SV"][label2])
                    else: 
                        scen_data["node"]["label"].append(translator["EN"][label2])
                    #Save the color to show
                    scen_data["node"]["color"].append(info_data[label2]["color"])
```
Later, it is calculated the percentage of the node in relation to the total energy. This value is displayed in the Sankey, but also used to determine the y-axis position. That's why for column 1 it is used sum energy production and for column 3 sum energy usage, and both are stored as strings for the Sankey. However, for column 2 there is no sum of energies to compare, so it is not display, and the y-axis is calculate approximately.
```python
                    if info_data[label2]["column"] == 1:
                        percentage_value = node_value/s_e_production
                        percentage_name = str(round(percentage_value,2)*100) + "%"

                    # Intermediate nodes (they do not display percentage)
                    elif info_data[label2]["column"] == 2:
                        percentage_value = node_value/s_e_production
                        percentage_name = ""

                    # Outputs nodes
                    elif info_data[label2]["column"] == 3:
                        percentage_value = node_value/s_e_usage
                        percentage_name = str(round(percentage_value,2)*100) + "%"

                    scen_data["node"]["percentage"].append(percentage_name)
```
Then, for x-axis possition they usually have a fixed position according to the column they belong. But, some special cases have been declared in All_Labels_Dictionary.
```python
                    if "x" in info_data[label2]:
                        scen_data["node"]["x"].append(info_data[label2]["x"])

                    elif info_data[label2]["column"] == 1:
                        scen_data["node"]["x"].append(0.001)

                    elif info_data[label2]["column"] == 2:
                        scen_data["node"]["x"].append(0.5)

                    elif info_data[label2]["column"] == 3:
                        scen_data["node"]["x"].append(1)
```
For y-axis position it is a bit more chaotic. 

On one hand, this code aims to be as generic and standardised as possible, so to meet the specific features of each municipality it is better to declare the same way as for x-axis the special cases for y-axis in All_Labels_Dictionary. So, firstly it checks if this y-special value exists.

On the other hand, it is supposed that Sankey function automatically place a space between the nodes, but it seems that when the value of the node is very small this feature it is not added. That's why I have implemented some extra code to add some space between those little values (that only appear in the first column). 

And the normal case, it will only take the previous position and add half of the width of the label. Because the y-axis it is implemented in the central point.

(Finally, i actualised to store the position of the next energy variable)

```python
                    if "y" in info_data[label2]:
                        scen_data["node"]["y"].append(info_data[label2]["y"])
                        
                    elif info_data[label2]["column"] == 1: 
                        if percentage_value > 0.05:
                            y[info_data[label2]["column"]] += percentage_value/2
                            scen_data["node"]["y"].append(y[info_data[label2]["column"]])
                            y[info_data[label2]["column"]] += (percentage_value/2 - 0.01)

                        else: 
                            y[info_data[label2]["column"]] += 0.015
                            scen_data["node"]["y"].append(y[info_data[label2]["column"]])
                            y[info_data[label2]["column"]] += percentage_value/2 + 0.015

                    else: 
                        y[info_data[label2]["column"]] += percentage_value/2
                        scen_data["node"]["y"].append(y[info_data[label2]["column"]])
                        y[info_data[label2]["column"]] += percentage_value/2

                    i += 1
```
### Declaration of link's data
All energy types that are shown in the Sankey are defined in node_positions. In this loop, this dictionary is run through to establish the connections between the energy types.

The energy types stored in node_positions include energies that do not have any connection because they are the tail (We have called them "outputs"). 

Then, links are only established for energy types that have connections (information inside "target"). The attribute "target" is running through (because one energy type can have more than 1 connection) and it is saved the name of the target and the name of the value (name where it is saved the value of the connection, not the same as the value of the target).

If target is in node_positions then the connection exists. So, the link is made by adding the associated numbers of the energy types correspondingly to the source and target attributes.

Next, the value of the link is searched. Then, it is treated if a change of the units is required. And finally, it is added to the dictionary. As well as the colour.

```python
for label in node_positions:
    if info_data[label]["target"] != ("link" and "output"):
        
        for a in range(len(info_data[label]["target"])):
            target_name = info_data[label]["target"][a]
            value_name = info_data[label]["value"][a]

            if target_name in node_positions.keys():
                
                target_position = node_positions[target_name]
                scen_data["link"]["target"].append(target_position)  
                scen_data["link"]["source"].append(node_positions[label])

                if ("T0 " + value_name) in scen_variables:
                    find_value = abs(scen_file["T" + str(year) + " " + value_name][num_row[0]])
                
                elif value_name in constant_variables:
                    find_value = constant_file[value_name][0]

                if unit == "mega":
                    find_value = find_value*1000

                elif unit == "kilo":
                    find_value = find_value*1000000

                scen_data["link"]["value"].append(find_value)
                scen_data["link"]["color"].append(info_data[value_name]["color"])
```
### Final part
Finally, the values of the sum energies are modified if necessary to mega or kilo, and rounded to display less decimals
```python
    if unit == "mega":
        s_e_production = s_e_production*1000
        s_e_usage = s_e_usage*1000

    elif unit == "kilo":
        s_e_production = s_e_production*1000000
        s_e_usage = s_e_usage*1000000

    s_e_production = round(s_e_production, 2)
    s_e_usage = round(s_e_usage, 2)
```