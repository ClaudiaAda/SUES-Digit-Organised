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