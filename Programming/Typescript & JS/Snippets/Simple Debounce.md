```function debounce(func, wait) {
    let timeout;

    return function() {
        const context = this;
        const args = arguments;

        clearTimeout(timeout);

        timeout = setTimeout(() => {
            func.apply(context, args);
        }, wait);
    };
}

// Usage example:
const handleResize = () => {
    console.log('Window resized');
};

const debouncedResize = debounce(handleResize, 500);

window.addEventListener('resize', debouncedResize);
```