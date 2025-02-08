To reference a Tailwind CSS animation defined in the `tailwind.config.js` file, follow these steps:

1. **Define the Animation in `tailwind.config.js`:**
    
    You can define custom animations in the `extend` section of the `tailwind.config.js` file under `keyframes` and `animation`.

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      keyframes: {
        wiggle: {
          '0%, 100%': { transform: 'rotate(-3deg)' },
          '50%': { transform: 'rotate(3deg)' },
        },
      },
      animation: {
        wiggle: 'wiggle 1s ease-in-out infinite',
      },
    },
  },
}

```

**Apply the Animation in Your Component:**

Use the `animate-` class prefix followed by your custom animation name in your HTML or JSX.


```html
<!-- Example in HTML -->
<div class="animate-wiggle">Wiggle Animation</div>

```


```tsx
// Example in JSX
const MyComponent = () => (
  <div className="animate-wiggle">
    Wiggle Animation
  </div>
);

```

1. **Ensure Tailwind CSS is Properly Configured:**
    
    Make sure Tailwind CSS is set up correctly in your project and that the `tailwind.config.js` file is recognized by your build process.
    

**Summary:**

- **Define** the animation in `tailwind.config.js` under `keyframes` and `animation`.
- **Reference** the animation in your HTML/JSX with `class="animate-[your-animation-name]"`.

This method leverages Tailwind's utility-first approach, allowing you to keep your styling consistent and maintainable.

