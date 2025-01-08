### . CSS Approach (Dynamic):

You can use CSS to visually resize an image when it is rendered in the browser, which doesn't actually change the image's file size but alters how it appears on the screen.


`function ResizedImageComponent({ src }) {   return (     <img src={src} alt="Resized Logo" style={{ width: '70px', height: '70px' }} />   ); }`

### 2. HTML Attributes (Dynamic):

Similar to the CSS approach but using HTML width and height attributes:


`function ResizedImageComponent({ src }) {   return (     <img src={src} alt="Resized Logo" width="70" height="70" />   ); }`

### 3. Canvas API (Dynamic and Actual):

If you want to actually resize the image data, you can use the HTML Canvas API to draw the image to a canvas element and then export the resized image. This method allows you to maintain the quality as much as possible and is done through a React ref.

```
import React, { useRef, useEffect } from 'react';

function ResizedImageComponent({ src }) {
  const canvasRef = useRef(null);

  useEffect(() => {
    const image = new Image();
    image.src = src;
    image.onload = () => {
      const canvas = canvasRef.current;
      canvas.width = 70;
      canvas.height = 70;
      const ctx = canvas.getContext('2d');
      ctx.drawImage(image, 0, 0, 70, 70);
    };
  }, [src]);

  return <canvas ref={canvasRef} style={{ display: 'none' }} />;
}

```
You can then convert the canvas data to a Blob or a Data URL if you need to use the resized image for uploads or downloads.

### 4. Using a Library (Dynamic or Build-time):

There are libraries available that can make resizing easier, like `react-image-file-resizer`, which handles resizing on the client side.


`npm install react-image-file-resizer`

Use the library within your React component:


`import Resizer from 'react-image-file-resizer';  function ResizedImageComponent({ src }) {   const [resizedImageSrc, setResizedImageSrc] = useState('');    useEffect(() => {     Resizer.imageFileResizer(       src,       70,`