## 方法

方法的语法和函数相似. 不同的是方法是在结构体(枚举或 trait 对象)的上下文中定义的, 且第一个参数总是
`self`.


### 定义方法

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

// 定义方法
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect = Rectangle { width: 30, height: 50, };

    println!("area {}", rect.area());
}
```

第一个参数 `&self` 表示调用该方法时将获取对象的不可变引用; 如果需要在方法中修改结构体成员,
则需要使用 `&mut self` 来获取对象的可变引用; 如果需要获取对象的所有权, 则使用 `self`.


> 在 C 和 C++ 中分别使用 `.` 和 `->` 来访问对象和指针的成员. 但是在 Rust 中没有 `->`, Rust
> 实现了称为 *自动引用和解引用* 的特性, 可以使用 `.` 来统一访问对象和引用的成员.


### 关联函数

在 `impl` 块中声明的, 而且没有 `self` 参数的函数.

```rust
impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle { width: size, height: size }
    }
}
```


### 多个 `impl` 块

可以在多个 `impl` 块中, 为同一个结构体定义方法或关联函数:

```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}
```

在这里, 我们没有理由把这两个方法分开定义, 但是它是合法的. 当使用泛型或实现 trait 时,
允许分开定义的语法特别有用.
