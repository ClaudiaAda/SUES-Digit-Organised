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

This file it is treated to store the energy types' names as the rows of the dataframe, so later we can use this value to find the translation. #Translator is the dictionary that stores this data.
        - `pd.read_csv`(""): Store the csv from the path indicated
        - `pd.DataFrame`(data, columns, index): Create a dataframe (table with the information attached)
```python
translator_dictionary = pd.read_csv("Latest Folder\libreria.csv")
rows = list(translator_dictionary["NAMES"])
data = list(translator_dictionary["SV"])
translator = pd.DataFrame(data, columns = ["SV"], index=rows)
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
y = [0,0.01,0.01,0.01] 

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
