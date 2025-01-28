Rust's approach includes:

1. Same memory alignment requirements as C
2. The `repr` attribute lets you control padding behavior:

```rust
// Default Rust alignment and padding
struct Normal {
    a: u8,    // 1 byte + padding
    b: i32,   // 4 bytes
}

// C-compatible layout
#[repr(C)]
struct LikeC {
    a: u8,    // 1 byte + padding
    b: i32,   // 4 bytes
}

// Pack fields tightly (can hurt performance!)
#[repr(packed)]
struct Packed {
    a: u8,    // 1 byte
    b: i32,   // 4 bytes, no padding before
}
```

The big difference is that Rust prevents many of the security vulnerabilities we discussed in C because:

1. No uninitialized memory
2. Memory safety guarantees
3. Explicit control over representation

Would you like to explore how Rust's type system prevents the padding-related vulnerabilities we discussed in C?