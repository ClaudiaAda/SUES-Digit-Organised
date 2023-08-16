# DICTIONARIES
To allow the creation of data that can be used by the Sankey function, it is needed to have a dictionary that stores the information of the energy types (name, colour, connections, positions,..): [all_labels_dictionary]

On the other hand, to handle translations to swedish or better english, it is used to tables/excel files to store this translations. One for the web page [AAAA] and other for the energy labels inside the Sankey [BBBB]

Next, it is explained how the information is displayed and how to add new elements to them.

## All_labels_dictionary
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
