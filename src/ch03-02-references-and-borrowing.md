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

我们称 "获取值的引用的行为" 作 *借用*. 例如将一个值的引用传递给函数, 相应的形参获取了这个值的引用,
称该形参借用了这个值.

> 关于借用的定义, 是我自己的理解, 不知道是否正确? 官方的说法有些模糊, 原文是这样的:
>
> We call having references as function parameters borrowing. As in real life, if a person owns
> something, you can borrow it from them. When you’re done, you have to give it back.
