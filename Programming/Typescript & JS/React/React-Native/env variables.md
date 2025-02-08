To add environment variables to a React Native project, you can use libraries like `react-native-config` which allow you to manage configuration settings and secret keys outside your codebase. Here’s how you can set it up:

1. **Install react-native-config**: You can install the `react-native-config` package using yarn (as it's your preferred package manager):

```bash
yarn add react-native-config

```
    
2. **Link the library**: If you are using a version of React Native lower than 0.60, you will need to link the library manually:
    
    
```bash
react-native link react-native-config

```
    
    For React Native 0.60 and higher, autolinking should take care of this step for you.
    
3. **Configuration Files**: Create a `.env` file in the root of your React Native project. This file will contain your environment variables:
    
  
```
API_URL=https://your-api-url.com
SECRET_KEY=your_secret_key

```
    
    You can create different `.env` files for different environments, like `.env.staging`, `.env.production`, etc.
    
4. **Accessing Environment Variables**: You can access these variables in your React Native code using the `react-native-config` library:

```bash
import Config from 'react-native-config';

console.log(Config.API_URL);  // Outputs: https://your-api-url.com

```
    
5. **iOS Specifics**:
    
    - Ensure you have a `ios/[YourProjectName]/.xcconfig` file for each environment (e.g., `Release.xcconfig` and `Debug.xcconfig`).
    - Include the `react-native-config` generated settings in these files:

```cpp
#include? "../../node_modules/react-native-config/ios/ReactNativeConfig.xcconfig"
```
1. **Android Specifics**:
    
    - Update the `android/app/build.gradle` file to apply the `react-native-config` plugin at the top:
        
    
		```c
apply plugin: "com.bugsnag.android.gradle"
apply from: project(':react-native-config').projectDir.getPath() + "/dotenv.gradle"

```
        
    - Make sure your `android/app/src/main/java/[...]/MainApplication.java` imports and uses the `Config` class if needed.
2. **Security Note**: Remember, although environment variables can keep sensitive keys out of your source code, they will still be bundled into the application when it's built and can potentially be accessed by extracting the APK or IPA file.
    

This setup helps maintain a cleaner codebase, separating configuration from code, which is especially useful when working across multiple development environments or when needing to protect sensitive data.