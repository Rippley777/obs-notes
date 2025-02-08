To enable shadows in `react-three-fiber`, you need to configure both the light sources and the objects to cast and receive shadows. Here's how you can set it up:

1. **Configure the Canvas**: Enable the shadow map in the `Canvas`.
    
2. **Set Up Lights**: Configure the lights to cast shadows.
    
3. **Configure Objects**: Set objects to cast and receive shadows.
    

Here's a complete example

```jsx
import React from 'react';
import { Canvas } from '@react-three/fiber';
import { OrbitControls, useGLTF } from '@react-three/drei';

function Model() {
  const { scene } = useGLTF('/path/to/your/model.gltf'); // Load your model

  // Enable casting and receiving shadows
  scene.traverse((object) => {
    if (object.isMesh) {
      object.castShadow = true;
      object.receiveShadow = true;
    }
  });

  return <primitive object={scene} />;
}

export default function App() {
  return (
    <Canvas shadows camera={{ position: [5, 5, 5], fov: 50 }}>
      {/* Lights */}
      <ambientLight intensity={0.5} />
      <directionalLight 
        position={[10, 10, 5]} 
        castShadow 
        shadow-mapSize-width={1024}
        shadow-mapSize-height={1024}
        shadow-camera-far={50}
        shadow-camera-left={-10}
        shadow-camera-right={10}
        shadow-camera-top={10}
        shadow-camera-bottom={-10}
      />

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

### Breakdown:

- **Canvas**: `shadows` prop enables shadow map rendering.
- **Directional Light**: `castShadow` enables shadow casting.
- **Mesh Configuration**:
    - `castShadow` prop on meshes to cast shadows.
    - `receiveShadow` prop on meshes to receive shadows.
- **Scene Traversal**: Iterate over all meshes in the model to set `castShadow` and `receiveShadow`.

### Notes:

- **Shadow Map Size**: Adjust `shadow-mapSize-width` and `height` for shadow resolution.
- **Shadow Camera**: Configure the shadow camera bounds (`left`, `right`, `top`, `bottom`) for optimal shadow rendering.
- 