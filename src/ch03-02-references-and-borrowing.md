## 引用与借用

我们可以使用引用来简化上一节的最后一个例子:

```rust
fn main() {
    let s = String::from("hello");

    let len = calculate_length(&s);

    println!("s: {}, len: {}", s, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

传递给 `calculate_length` 的实参是 `&s`, 其形参类型是 `&String`, 这里的 `&` 就是*引用*. 我们称 `&s`
是一个指向 `s` 的引用, 引用并不拥有值的所有权, 所以当引用离开作用域时, 不会丢弃它指向的值. `&String`
是类型 `String` 的引用类型.

我们把 "获取值的引用的行为" 称为 *借用*. 例如将一个值的引用传递给函数, 相应的形参获取了这个值的引用,
称该形参借用了这个值.

> 关于借用的定义, 是我自己的理解, 不知道是否正确? 官方的说法有些模糊, 原文是这样的:
>
> We call having references as function parameters borrowing. As in real life, if a person owns
> something, you can borrow it from them. When you’re done, you have to give it back.


### 可变引用

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

可变引用 `&mut s`, 可变引用类型 `&mut String`. 可变引用指向的变量也必须是可变的.
不允许同时有多个有效的可变引用指向同一个变量.

```rust
let mut s = String::from("hello");

{
    let r1 = &mut s;

} // r1 离开作用域, 所以接下来我们还可以创建 s 的可变引用

let r2 = &mut s;
```

不允许同时存在同一个变量的有效的不可变引用和可变引用.

```rust
let mut s = String::from("hello");

let r1 = &s;
let r2 = &s;
println!("{} and {}", r1, r2);
// r1 和 r2 在这之后不再使用了, 所以接下来可以创建 s 的可变引用

let r3 = &mut s;
println!("{}", r3);
```


### 悬垂引用

Rust 可以保证不会出现当一个值被丢弃还能使用其引用的情况:

```rust
fn dangle() -> &String {
    let s = String::from("hello");

    &s
}
```

`s` 因为离开作用域, 在函数返回前被丢弃, 该函数返回了一个无效的值的引用, 这是不能编译的.


### 引用规则

* 任何时候, 只能拥有一个可变引用或多个不可变引用.
* 引用必须指向有效的值.
