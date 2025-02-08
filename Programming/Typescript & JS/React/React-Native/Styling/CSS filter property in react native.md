In React Native, you can achieve effects similar to the CSS `filter` property by using various style properties directly in your components. Specifically, to mimic `saturate(0)` (which desaturates an image to grayscale) and `brightness(1.2)` (which increases the brightness), you can use a combination of `tintColor` and manipulating the `Image` component's properties.

Here's a way to simulate these effects:

1. **Desaturation (Grayscale)** - React Native does not directly support a saturation filter, so you would typically handle this by editing the image beforehand or using a library that processes the image to grayscale.
    
2. **Brightness** - To adjust the brightness, you can overlay the image with a semi-transparent white or black view, depending on whether you want to make the image brighter or darker. However, this is a rudimentary approach and may not give perfect results.
    

For more precise control, you might consider using a third-party library like `react-native-image-filter-kit`, which offers a variety of image processing filters similar to CSS. Here's an example using `react-native-image-filter-kit` to apply desaturation and brightness:


```javascript
import React from 'react';
import { Image } from 'react-native';
import { Grayscale, Brightness } from 'react-native-image-filter-kit';

const FilteredImage = ({ source }) => {
  return (
    <Brightness
      amount={1.2}
      image={
        <Grayscale
          amount={1.0}
          image={
            <Image
              style={{ width: 200, height: 200 }}
              source={source}
            />
          }
        />
      }
    />
  );
};

export default FilteredImage;

```

In this example, the `Grayscale` component from `react-native-image-filter-kit` applies the grayscale effect, and the `Brightness` component adjusts the brightness. Adjust the `amount` as needed to get the desired effect.

Keep in mind that these libraries may have performance implications, especially if used on large images or in lists.