## match 控制流

`match` 用于匹配一个值的模式, 并执行相应的代码. 编译器保证这个值的所有模式都被处理.

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```

`match` 之后是一个表达式(其值可以是任意类型), 分支位于紧接着的 `{}` 中. `match`
表达式的每个分支称为一个 `臂(arm)`, `=>` 的前后分别是模式和代码, `臂` 之间使用 `,` 隔开. 当 `match`
表达式执行时, 按照 `臂` 的顺序匹配表达式的值与 `臂` 的模式. 如果成功匹配, 则执行相应的代码.

`臂` 的代码是一个表达式, 如果该臂被匹配到, 则其值就是整个 `match` 表达式的返回值.


### 绑定值的模式

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}

let none: Option<i32> = None;
println!("{:?}", none);
println!("{:?}", plus_one(Some(5)));
```


### `_` 通配符

正如开始所说, 编译器需要保证值的所有模式都被处理. 当我们希望剩余的模式都统一处理的时候, 可以使用
`_`, 它匹配所有模式:

```rust
let some_u8_value = 1u8;
match some_u8_value {
    1 => println!("one"),
    2 => println!("two"),
    _ => (),
}
```
