## `if let` 控制流

当我们只希望处理一个模式而忽略其它模式时, 使用 `if let` 比较简洁:

```rust
let some_u8_value = Some(2u8);

if let Some(2) = some_u8_value {
    println!("two");
}

if let Some(i) = some_u8_value {
    println!("{}", i);
} else {
    println!("None");
}
```
