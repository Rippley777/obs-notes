


## Troubleshoot 

If the lighting is not working in `react-three-fiber`, there are several things you can check and adjust to troubleshoot and resolve the issue:

### Checklist and Steps to Fix Lighting Issues

1. **Ensure Lights are Added Properly**:
    
    - Verify that light components are correctly added to the scene.
2. **Verify Light Positioning and Intensity**:
    
    - Make sure lights are positioned properly and have sufficient intensity.
3. **Check Materials**:
    
    - Ensure materials on objects are compatible with lighting (e.g., `meshStandardMaterial`).
4. **Enable Shadows Properly**:
    
    - Ensure shadows are correctly set up if needed.
5. **Update and Traverse Scene Objects**:
    
    - Make sure objects are set to receive and cast shadows.

### Example with Detailed Setup

Here’s a detailed example ensuring all aspects are covered:

```jsx
import React, { useEffect } from 'react';
import { Canvas } from '@react-three/fiber';
import { OrbitControls, useGLTF } from '@react-three/drei';

function Model() {
  const { scene } = useGLTF('/path/to/your/model.gltf');

  useEffect(() => {
    scene.traverse((object) => {
      if (object.isMesh) {
        object.castShadow = true;
        object.receiveShadow = true;
        // Ensure the material is compatible with lighting
        if (object.material) {
          object.material.needsUpdate = true;
        }
      }
    });
  }, [scene]);

  return <primitive object={scene} />;
}

export default function App() {
  return (
    <Canvas shadows camera={{ position: [5, 5, 5], fov: 50 }}>
      {/* Ambient Light */}
      <ambientLight intensity={0.5} />
      
      {/* Directional Light */}
      <directionalLight 
        position={[10, 10, 5]} 
        intensity={1}
        castShadow 
        shadow-mapSize-width={1024}
        shadow-mapSize-height={1024}
        shadow-camera-far={50}
        shadow-camera-left={-10}
        shadow-camera-right={10}
        shadow-camera-top={10}
        shadow-camera-bottom={-10}
      />

      {/* Point Light (optional) */}
      <pointLight position={[5, 5, 5]} intensity={0.5} />

      {/* Ground */}
      <mesh receiveShadow rotation={[-Math.PI / 2, 0, 0]} position={[0, -1, 0]}>
        <planeBufferGeometry args={[100, 100]} />
        <meshStandardMaterial color="lightgray" />
      </mesh>

      {/* Model */}
      <Model />

      <OrbitControls />
    </Canvas>
  );
}

```

### Key Points:

- **Lights**: Ensure at least one light (e.g., `ambientLight`, `directionalLight`, `pointLight`) is added with appropriate intensity.
- **Positioning**: Lights should be positioned such that they illuminate the objects.
- **Shadows**:
    - Enable shadows in `Canvas` (`shadows` prop).
    - Ensure lights casting shadows have `castShadow` set to `true`.
    - Set `castShadow` and `receiveShadow` on relevant meshes.
- **Materials**: Use materials that interact with light, such as `meshStandardMaterial`.

### Troubleshooting Tips:

- **Increase Light Intensity**: Sometimes the default intensity might be too low.
- **Check Light Direction**: Ensure the light is directed towards the objects.
- **Verify Shadow Settings**: Ensure shadow camera settings cover the area of interest.
