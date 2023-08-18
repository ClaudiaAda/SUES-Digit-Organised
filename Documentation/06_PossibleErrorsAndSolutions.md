# POSSIBLE ERRORS AND SOLUTIONS
In this file it is going to explain some of the possible errors that can appear when executing the program.

## Errors with excel files
If in the webpage appears an error like this:

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/images/error1.png)
If it says "list index out of range", it is usually because it could not read the excel file. This can happen because the delimiters changed.

For [scenarios](https://github.com/ClaudiaAda/SUES-Digit-Organised/tree/main/1.%20EXECUTABLE/Scenarios), the delimiter has to be ",". Sometimes, when this files are open in excel and then save it, the delimiter will change to ";" so it won't be able to be opened in the program later. If it is wanted to change the delimiter from "," to ";" of all scenarios files, it is necessary to change this lines in [A_main](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/1.%20EXECUTABLE/A_main.py) so the program can work (add: delimiter=";")

Before:
```
    if peak_hour == ['PeakHour']:
        scen_file = pd.read_csv("Scenarios/vensim_data_Scen"+scenario+"_"+peak_hour[0]+winter_summer+"_"+kommun+"_ver.csv" )
    else:
        scen_file = pd.read_csv("Scenarios/vensim_data_Scen"+scenario+"_"+kommun+"_ver.csv" )
```

After:
```
    if peak_hour == ['PeakHour']:
        scen_file = pd.read_csv("Scenarios/vensim_data_Scen"+scenario+"_"+peak_hour[0]+winter_summer+"_"+kommun+"_ver.csv", delimeter=";" )
    else:
        scen_file = pd.read_csv("Scenarios/vensim_data_Scen"+scenario+"_"+kommun+"_ver.csv", delimeter=";")
```

For [E_Language_Dictionary](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/1.%20EXECUTABLE/E_Language_Dictionary.csv) and  [F_Sankey_Language_Dictionary](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/1.%20EXECUTABLE/F_Sankey_Language_Dictionary.csv) it is the opposite the delimeter in their files is ";" and the functions that read them have already this delimiter included. If it is changed to "," in their excel files they won't work.

## Errors with no existing files
Sometimes it can appear errors in the web page because it is possible to select all features for all options, but it not all options exists. For example, Scen5 and Scen6 do not have peak_hour information, so if you select them this error will happen.

![](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/images/error2.png)

## Errors when adding new energies
It is important to follow the steps described in [04_DictionariesDocumentation](https://github.com/ClaudiaAda/SUES-Digit-Organised/blob/main/Documentation/04_DictionariesDocumentation.md), errors can happen because energies can be introduced in some dictionaries, but not in others.

## Errors in the code
Errors can also appear because in some functions, different line codes or declarations of attributes have to be separated by comas, meanwhile in other put comas give errors and the separation is only the line break.



