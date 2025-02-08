# Game Development in Rust: A Quick Deep Dive

## 1. Setting Up Your Rust Game Development Environment

First, ensure you have Rust installed:

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

You'll also need `cargo`, Rust's package manager, which comes with Rust.

For game development, install some essential Rust crates:

```sh
cargo install cargo-watch
```

### Choosing a Game Engine/Framework

| Engine/Framework | Description |
|-----------------|-------------|
| Bevy | Data-driven ECS engine, minimal boilerplate |
| Amethyst | ECS-based, more feature-rich but heavier |
| Macroquad | Simple, lightweight, ideal for small projects |
| GGEZ | Inspired by LÖVE, great for 2D games |

## 2. Creating a Bevy Game (Recommended for Modern ECS)

```sh
cargo new my_bevy_game --bin
cd my_bevy_game
cargo add bevy
```

Modify `main.rs`:

```rust
use bevy::prelude::*;

fn main() {
    App::new()
        .add_plugins(DefaultPlugins)
        .add_startup_system(setup)
        .run();
}

fn setup(mut commands: Commands) {
    commands.spawn(Camera2dBundle::default());
}
```

Run the game:

```sh
cargo run
```

## 3. Adding an Entity (Player)

Modify `setup` to spawn a player sprite:

```rust
fn setup(mut commands: Commands, asset_server: Res<AssetServer>, mut materials: ResMut<Assets<ColorMaterial>>) {
    commands.spawn(Camera2dBundle::default());
    
    let texture_handle = asset_server.load("player.png");
    commands.spawn(SpriteBundle {
        texture: texture_handle,
        transform: Transform::from_xyz(0.0, 0.0, 0.0),
        ..Default::default()
    });
}
```

## 4. Adding Player Movement

Create a new system:

```rust
fn player_movement(
    keyboard_input: Res<Input<KeyCode>>,
    mut query: Query<&mut Transform, With<Player>>,
) {
    let mut transform = query.single_mut();
    let speed = 2.0;
    
    if keyboard_input.pressed(KeyCode::W) {
        transform.translation.y += speed;
    }
    if keyboard_input.pressed(KeyCode::S) {
        transform.translation.y -= speed;
    }
    if keyboard_input.pressed(KeyCode::A) {
        transform.translation.x -= speed;
    }
    if keyboard_input.pressed(KeyCode::D) {
        transform.translation.x += speed;
    }
}
```

Then, register the system:

```rust
fn main() {
    App::new()
        .add_plugins(DefaultPlugins)
        .add_startup_system(setup)
        .add_system(player_movement)
        .run();
}
```

## 5. Handling Game Logic (Collision Detection Example)

For simple AABB collision detection:

```rust
fn check_collisions(mut query: Query<(&Transform, &Sprite), With<Player>>) {
    for (transform, sprite) in query.iter() {
        let player_size = sprite.custom_size.unwrap_or(Vec2::new(32.0, 32.0));
        if transform.translation.x > 100.0 { // Example boundary
            println!("Collision detected!");
        }
    }
}
```

Register the system:

```rust
.add_system(check_collisions)
```

## 6. Adding a Game Loop

Bevy automatically runs a game loop. You can control update logic with:

```rust
fn game_update(mut state: ResMut<State<GameState>>) {
    println!("Game updating...");
}
```

## 7. Building for Web (WASM)

```sh
rustup target add wasm32-unknown-unknown
cargo install wasm-bindgen-cli
cargo build --target wasm32-unknown-unknown
```

Use `wasm-server-runner` for local testing:

```sh
cargo install wasm-server-runner
cargo run --target wasm32-unknown-unknown
```

## 8. Resources to Go Further

- [Bevy Official Docs](https://bevyengine.org/)
- [Rust GameDev WG](https://gamedev.rs/)
- [Are We Game Yet?](https://arewegameyet.rs/)

## Conclusion

Rust is an excellent language for game development with its safety, performance, and modern features. Bevy is an easy-to-learn, powerful framework that simplifies game development while leveraging Rust’s strengths.

---

🔥 Get coding, and let me know if you need deeper dives into physics, shaders, networking, or other advanced topics!
