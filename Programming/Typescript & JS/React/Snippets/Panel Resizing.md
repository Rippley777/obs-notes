
```tsx
import React, { useState } from "react";

const ResizablePanel: React.FC = () => {
  const [panelWidth, setPanelWidth] = useState(300); // Initial width of the panel
  const [isResizing, setIsResizing] = useState(false);

  const startResizing = (e: React.MouseEvent) => {
    e.preventDefault();
    setIsResizing(true);
  };

  const stopResizing = () => {
    setIsResizing(false);
  };

  const resize = (e: MouseEvent) => {
    if (isResizing) {
      const newWidth = e.clientX;
      setPanelWidth(newWidth);
    }
  };

  React.useEffect(() => {
    if (isResizing) {
      document.addEventListener("mousemove", resize);
      document.addEventListener("mouseup", stopResizing);
    } else {
      document.removeEventListener("mousemove", resize);
      document.removeEventListener("mouseup", stopResizing);
    }

    return () => {
      document.removeEventListener("mousemove", resize);
      document.removeEventListener("mouseup", stopResizing);
    };
  }, [isResizing]);

  return (
    <div style={{ display: "flex", height: "100vh" }}>
      <div style={{ width: `${panelWidth}px`, background: "#f4f4f4" }}>
        Resizable Panel
      </div>
      <div
        onMouseDown={startResizing}
        style={{
          width: "5px",
          cursor: "col-resize",
          background: "#ddd",
        }}
      />
      <div style={{ flex: 1, background: "#e4e4e4" }}>Main Content</div>
    </div>
  );
};

export default ResizablePanel;

```

- **State Management**: `panelWidth` controls the width of the resizable panel.
- **Mouse Events**: Handlers for resizing:
    - `mousedown`: Start resizing.
    - `mousemove`: Adjust width dynamically.
    - `mouseup`: Stop resizing.
- **Cleanup**: Remove listeners when resizing stops or component unmounts.

### **Adding More Features**

- **Touch Support**: Add similar handlers for `touchstart`, `touchmove`, and `touchend`.