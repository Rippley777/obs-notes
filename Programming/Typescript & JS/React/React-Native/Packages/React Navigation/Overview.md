To add routing to a React Native app, you can use React Navigation, which is one of the most popular libraries for handling navigation in React Native applications. It allows you to handle transitions between different screens smoothly and provides a lot of flexibility and customization options.

Here’s how you can add routing to the app using React Navigation:

### Step 1: Install React Navigation

First, you need to install the necessary packages. Open your terminal in your project directory and run:


```bash
npm install @react-navigation/native

```

React Navigation also depends on the React Native Gesture Handler, React Native Reanimated, React Native Screens, React Native Safe Area Context, and React Native Masked View. You can install these dependencies using:


```bash
npm install react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-masked-view/masked-view

```
For Expo managed projects, these libraries might already be included, or you can use:



```bash
expo install react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-masked-view/masked-view

```
### Step 2: Set Up Navigation Stack

For most apps, a stack navigator is a common choice. It allows users to open new screens and go back to previous ones. Install the stack navigator library:


```bash
npm install @react-navigation/stack

```
### Step 3: Configure the Navigator

Create a new file for your navigator, e.g., `AppNavigator.js`, and set up your stack navigator:


```javascript
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './HomeScreen'; // your main screen
import DetailsScreen from './DetailsScreen'; // another screen you might navigate to

const Stack = createStackNavigator();

function AppNavigator() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} options={{ title: 'Overview' }} />
        <Stack.Screen name="Details" component={DetailsScreen} options={{ title: 'Details' }} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default AppNavigator;

```
### Step 4: Update the App Entry Point

Update your `App.js` to use the `AppNavigator`:



```javascript
import React from 'react';
import AppNavigator from './AppNavigator';

export default function App() {
  return <AppNavigator />;
}

```
### Step 5: Linking Between Screens

In your screens, you can now navigate between them using the navigation prop automatically provided by the stack navigator:


```javascript
import React from 'react';
import { Button, Text, View } from 'react-native';

const HomeScreen = ({ navigation }) => {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Home Screen</Text>
      <Button
        title="Go to Details"
        onPress={() => navigation.navigate('Details')}
      />
    </View>
  );
};

export default HomeScreen;

```

This is a basic setup. React Navigation provides a wide range of functionalities like passing parameters to routes, configuring the header bar, tab navigators, drawer navigators, and much more, which you can explore depending on your application's requirements.


## Using TypeScript
Typing the navigation prop in React Native with TypeScript when using React Navigation involves defining the types for the navigation parameters and actions. This provides type safety when navigating between screens and accessing route parameters. React Navigation provides a set of TypeScript types you can utilize for this purpose.

Here's a detailed guide on how to type the navigation prop using TypeScript:

### Step 1: Define Your Route Parameters

For each screen, you can define the expected parameters. If a screen doesn't receive any parameters, you can specify an empty object. Here’s an example of defining route parameters for a hypothetical app:



```tsx
type RootStackParamList = {
  Home: undefined;  // No parameters expected for the Home screen
  Details: { itemId: number, otherParam: string };  // Parameters for the Details screen
};

```
### Step 2: Use Typed Navigation Hooks

React Navigation offers several hooks like `useNavigation`, `useRoute`, and `useNavigationState` that can be typed with your parameter list:



```tsx
import { createStackNavigator, StackNavigationProp } from '@react-navigation/stack';
import { RouteProp } from '@react-navigation/native';
import { NavigationContainer } from '@react-navigation/native';
import { TypedNavigator, StackNavigationHelpers } from '@react-navigation/native';

const Stack = createStackNavigator<RootStackParamList>();

export type HomeScreenNavigationProp = StackNavigationProp<RootStackParamList, 'Home'>;
export type DetailsScreenRouteProp = RouteProp<RootStackParamList, 'Details'>;

// Component using the navigation prop
type HomeScreenProps = {
  navigation: HomeScreenNavigationProp;
};

const HomeScreen: React.FC<HomeScreenProps> = ({ navigation }) => {
  return (
    <Button
      title="Go to Details"
      onPress={() => navigation.navigate('Details', { itemId: 42, otherParam: 'anything' })}
    />
  );
};

```

### Step 3: Typing Component Props with Navigation and Route

For screens that need to access both navigation and route parameters, you can extend the component's props to include both:


```tsx
import React from 'react';
import { View, Text, Button } from 'react-native';
import { useRoute } from '@react-navigation/native';

// Details screen props
type DetailsScreenProps = {
  navigation: StackNavigationProp<RootStackParamList, 'Details'>;
  route: DetailsScreenRouteProp;
};

const DetailsScreen: React.FC<DetailsScreenProps> = ({ route, navigation }) => {
  const { itemId, otherParam } = route.params;

  return (
    <View>
      <Text>Item ID: {itemId}</Text>
      <Text>Other Param: {otherParam}</Text>
      <Button
        title="Go back"
        onPress={() => navigation.goBack()}
      />
    </View>
  );
};

```
### Step 4: Configuring Navigation Container and Stack Navigator

Make sure to wrap your app's entry point with `NavigationContainer` and configure your `StackNavigator`:



```tsx
const AppNavigator: React.FC = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Details" component={DetailsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
};

export default AppNavigator;

```
By following these steps, you effectively type-check the navigation and route usage in your app, leveraging TypeScript's capabilities to enhance code quality and reduce runtime errors related to navigation.