# Navigation

In order to make the navigation customizable I have split it up in two parts.
1. The actual navigation structure:
This is implemented in a json structure of which you can find an example in navigation/navigation.json
2. The display part:
This can become more complicated and is implemented with a vue component.
The component must take the json structure as argument and display its content.

The navigation component to use cannot be picked in the admin panel yet. instead you can change it by changing the code in navigation/default.vue for now.