```rust
use bevy::{
    prelude::*,
    window::{PresentMode, WindowMode, WindowPlugin, WindowResolution},
};
use raw_window_handle::{HasRawWindowHandle, RawWindowHandle};

fn main() {
    App::new()
        .add_plugins(DefaultPlugins.set(WindowPlugin {
            primary_window: Some(Window {
                title: "Rusty's Retirement Clone".to_string(),
                resolution: WindowResolution::new(400.0, 300.0),
                transparent: true,
                decorations: false,
                present_mode: PresentMode::AutoNoVsync,
                mode: WindowMode::Borderless,
                ..Default::default()
            }),
            ..Default::default()
        }))
        .add_startup_system(setup)
        .add_system(update_idle_worker)
        .run();
}

fn setup(mut commands: Commands, asset_server: Res<AssetServer>, mut materials: ResMut<Assets<ColorMaterial>>) {
    commands.spawn(Camera2dBundle::default());

    // Load texture
    let texture_handle = asset_server.load("textures/worker.png");
    commands.spawn(SpriteBundle {
        texture: texture_handle,
        transform: Transform::from_xyz(0.0, 0.0, 0.0),
        ..Default::default()
    });

    // Worker entity with idle job
    commands.spawn((Worker { resources_collected: 0 },));
}

#[derive(Component)]
struct Worker {
    resources_collected: u32,
}

fn update_idle_worker(mut query: Query<&mut Worker>, time: Res<Time>) {
    for mut worker in query.iter_mut() {
        worker.resources_collected += (time.delta_seconds() * 10.0) as u32;
        println!("Resources collected: {}", worker.resources_collected);
    }
}

#[cfg(target_os = "windows")]
#[no_mangle]
pub extern "system" fn raw_window_handle(window: &bevy::window::Window) -> RawWindowHandle {
    use windows::Win32::UI::WindowsAndMessaging::*;
    use windows::Win32::Foundation::HWND;
    
    let hwnd = HWND(window.raw_window_handle().unwrap().get_hwnd().unwrap());
    unsafe {
        SetWindowLongPtrW(hwnd, GWL_EXSTYLE, WS_EX_LAYERED.0 as isize);
        SetLayeredWindowAttributes(hwnd, 0, 255, LWA_ALPHA);
    }
    window.raw_window_handle().unwrap()
}

#[cfg(target_os = "linux")]
fn configure_wayland_x11(window: &bevy::window::Window) {
    use smithay_client_toolkit::window::{Decorations, WindowConfig};
    
    let handle = window.raw_window_handle().unwrap();
    if let RawWindowHandle::Wayland(_) = handle {
        println!("Configuring Wayland transparency...");
        // Wayland-specific transparency handling here
    } else if let RawWindowHandle::Xlib(_) = handle {
        println!("Configuring X11 transparency...");
        // X11-specific transparency handling here
    }
}

```