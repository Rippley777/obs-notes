In React Navigation, which is commonly used with React Native for handling navigation, you can change the header background color by setting the `options` prop on the `Stack.Screen` component. Here’s how you can do it:

Assuming you are using `@react-navigation/stack`, you would typically set up your navigator and screens something like this:


```javascript
import * as React from 'react';
import { createStackNavigator } from '@react-navigation/stack';
import { HomeScreen, DetailsScreen } from './Screens'; // Assume these are imported

const Stack = createStackNavigator();

function MyStack() {
  return (
    <Stack.Navigator>
      <Stack.Screen 
        name="Home" 
        component={HomeScreen}
        options={{ 
          headerStyle: {
            backgroundColor: '#f4511e', // Set your desired color
          },
          headerTintColor: '#fff', // Set the color of the header text and icons
          headerTitleStyle: {
            fontWeight: 'bold',
          },
        }}
      />
      <Stack.Screen 
        name="Details" 
        component={DetailsScreen}
        options={({ navigation, route }) => ({
          headerStyle: {
            backgroundColor: '#6a51ae', // Different color for this screen
          },
          headerTintColor: '#fff',
        })}
      />
    </Stack.Navigator>
  );
}

```
### Key points in the options:

- `headerStyle`: Controls the styling of the header. You can set the `backgroundColor` here to change the background color of the header.
- `headerTintColor`: Changes the color of the back button and title (if specified).
- `headerTitleStyle`: Used to style the title text, such as setting the font weight.

These options can be set directly on each screen or even dynamically based on screen props or state, allowing for flexible configuration of each screen's appearance within your navigator.