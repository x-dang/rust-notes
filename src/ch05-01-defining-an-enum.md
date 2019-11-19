## 定义枚举

```rust
enum IpAddrKind {
    V4,
    V6,
}

let ipv4 = IpAddrKind::V4;
```

枚举类型的成员可以关联数据, 你可以定义一个这样的枚举类型:

```rust
enum IpAddr {
    V4(String),
    V6(String),
}

let ipv6 = IpAddr::V6(String::from("::1"));
```

成员关联的数据类型不必要相同的:

```rust
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}

let ipv4 = IpAddr::V4(127, 0, 0, 1);
```

再让我们来定义一个包含多种成员的枚举类型:

```rust
enum Message {
    Quit,                       // 没有关联数据
    Move { x: i32, y: i32 },    // 包含一个匿名结构体
    Write(String),              // 包含一个 String
    ChangeColor(i32, i32, i32), // 包含三个 i32
}
```

和结构体一样, 你可以使用 `impl` 在枚举类型上定义方法:

```rust,ignore
impl Message {
    fn call(&self) {
        // --snip--
    }
}

let msg = Message::Move{ x: 0, y: 1};
msg.call();
```
