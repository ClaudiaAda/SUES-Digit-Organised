# DICTIONARIES
To allow the creation of data that can be used by the Sankey function, it is needed to have a dictionary that stores the information of the energy types (name, colour, connections, positions,..): [D_All_labels_dictionary]

On the other hand, to handle translations to swedish or better english, it is used to tables/excel files to store this translations. One for the web page [E_Language_Dictionary] and other for the energy labels inside the Sankey [F_Sankey_Language_Dictionary].

Next, it is explained how the information is displayed and how to add new elements to them.

## D_All_labels_dictionary (delimeter=",")
It is a dictionary of dictionaries. It has the information of ALL existing energy types of all municipalities. It is where add new information if new energy types or municipalities are implemented.

First keys are the names of the energy types (🚧 THE NAMES USED IN VENSIM, the ones that will appear as column names in the excel files generated 🚧).

Inside this keys, other dictionary is open. It stores keys with the attributes of each energy type.
> There is no specific order to declare the attributes inside this little dictionary, it does not make any change or error
To understand the connections and how the different energy types work -> let's make a declaration of 3 different types:

- Normal: Its name appears in the visualisation and has connections with other labels.
- Link: Its name does not appear in the visualisation, its value is used for the connection of other labels.
- Output: Its name appears, but its value is not used in the Diagram, as it is the final target.

The type of each energy is easily recognisable by looking at the "target" attribute. If it is a link or output type, that word will appear inside "target". If it is a normal type, "target" attribute will contain other energies's names. Examples:

#### Link Type
```
"DHP sum input energy": {
    "color": "rgba(0,255,1,0.4)",
    "target": "link"
}
```
#### Output Type
```
"distribution losses": {
    "color": "white",
    "target": "output",
    "column": 3 
}
```
#### Normal Type
```
"sum electric energy production EEP": {
    "color": "rgba(255,127,0,0.4)",
    "target": [
        "electric energy export",
        "distribution losses",
        "sum energy use homes",
        "sum energy use others",
        "sum energy use Public",
        "sum energy use Agriculture and forrestry",
        "sum energy use Industry",
        "sum energy use Transports"
    ],
    "value": [
        "electic energy import",
        "distribution losses from EEP",
        "electricity homes",
        "electricity others",
        "electricity Public",
        "electricity Agriculture and forrestry",
        "electricity Industry",
        "electricity Transports"
    ],
    "column": 2,
    "x": 0.6
}
```

As it can be seen in the examples, not all attributes can be used in all types. Let's explain the attributes, where they can be used and which information they store.

### target
It has been already explained. It is the most important, used in all types is the one who defines the type.
> "target" = "link"|"output"|"energy target name"

### value
Only used in normal types. It is the value for the connection between the energy source and the energy target specified.
🚧IMPORTANT! THE ORDER OF THE NAMES' VALUES HAS TO BE IN ACCORDANCE WITH THE ORDER OF THE TARGETS' NAMES🚧
> "value" = "energy value name"

### color
Used in normal and link types, it stores a rgba value that define the color that the sankey will display in nodes (normal) and links (link). 
> "color" = "rgba(red,green,blue,opacity) 
Change red, green and blue for a value between 0 and 255. And opacity between 0 and 1.

### column
Used in normal and outputs. They store the position where the energy appears.
> "column" = 1|2|3
1 is for the energies that appear in the left, 2 for the middle part and 3 for the right.
Each column has a predefined position.

### x|y
Used in normal and outputs (optional). It is only used in special cases, when it is wanted that the energy has a position that it is not the predefined. It can be defined "x" attribute, "y" attribute, both or none.
> "x" = number 
> "y" = number
Number is a value between [0.001, 1] 

### 🚧 HOW TO ADD NEW ELEMENTS?
When a new energy is going to be used, it is necessary to include it here in [D_All_Labels_Dictionary], as well as in [F_Sankey_Language_Dictionary] (if it is not declare in F, it will not display the name later).

For [D_All_Labels_Dictionary], it is important to have some points on mind to add the new energies correctly: 
 - 1. Use the same name as the one in the Vensim program for the keys of the dictionary.

 - 2. Define the type of the energy (normal|link|output):

    - Normal: If it is normal (its node goes to another node), we will have to see to which energies is connected and write them in "target". If it has only one target, then the "value" it is usually going to be itself so the same name as the key is added to "value". If it has more than one target, then it is necessary to see in which energy name is store the value of the connection and add that name to "value". Normal energies are required to have at least "target", "value", "column" and "color" attributes.

    - Link: The energy names that have been added in the attribute "value" of the normal types, have to be also added like a link type. Link energy are required to have only "target" and "color".

    - Output: The energy names that have been added in the attribute "target" of the normal types, that do not have more connections, they are a final node, they have to be added like a output type. Output energy are required to have at least "target", "color" and "column".

 - 3. Location: It is important to place correctly the new energies inside the dictionary because the order from top to bottom in which energies are displayed in the Sankey depend of this position in the dictionary. In reality, you have to be aware of the "relative" positions, to put it before or after of the energies that have the same column number.


## E_Language_Dictionary (delimeter=";")
It is a table(excel file) that stores the names of the web page elements. It has 3 columns: "ID","EN","SV".

In ID is saved the id of the object, in the other columns is the correspondient text in each language (English and Swedish).

### 🚧 HOW TO ADD NEW ELEMENTS?
If a new web page object it is added [A_main] file and it is wanted that the text displayed can change then:
 - 1. This object has to have an id.
 - 2. Add this id to the callback 
 ```
 Output("id","children")
 ```
    before the function:
 ```
 def language_translator(language):
    return [language_dictionary[language][word] for word in range(len(language_dictionary["ID"]))]
 ``` 
 - 3. Then update [E_Language_Dictionary] with this new id in "ID" column, and the correspondient translations in the other columns.

🚧It is important that the order of the ids in "ID" column in the excel file matches the order in which they are call in the callback (Outputs order).🚧

## F_Sankey_Language_Dictionary (delimeter=";")
The names of the energies display in the Sankey are saved in this other table. It has 3 columns: "NAMES","EN","SV". 

### 🚧 HOW TO ADD NEW ELEMENTS?
After adding a new energy to [D_All_Labels_Dictionary] the name has to be added to this dictionary. The order of the names does not matter, but 🚧it is important that in the column "NAMES" it is saved the same name as the one used in Vensim🚧. In the other 2 columns, it is store the name that is wanted to be displayed for each language. 
> (17/08/2023) At the moment, the translations are not declared correctly. They have to be changed to the ones desired.