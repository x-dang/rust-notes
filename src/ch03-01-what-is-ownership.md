## 什么是所有权

所有程序都需要在运行时它们管理使用的内存. 有些语言提供了垃圾回收功能, 并不时地检查不再使用的内存;
有些语言需要程序员手动地申请和释放内存. Rust 则使用第三种方式: 通过所有权系统管理内存,
其通过一系列的规则, 在编译时检查内存的使用情况. 所有权系统并不会减慢程序的运行速度.


### 所有权规则

* 每个值都有一个被称为 *所有者*(owner) 的变量.
* 每个值同时只能有一个所有者.
* 当所有者离开作用域, 该值将被丢弃.


### 变量作用域

变量作用域就是程序中变量有效的范围.

```rust
{                      // s 在这里无效, 它还没有被定义
    let s = "hello";   // s 从这里开始有效

    // do stuff with s
}                      // 该作用域在这里已结束, s 不再有效
```


### 内存分配

在 ["数据类型"](ch02-02-data-types.md) 那节介绍的类型都是存储在栈上的, 并在离开作用域时从栈上弹出.
一个存储在堆上的数据类型的例子是 `String`, 它可以存储变长的字符串. 下面的代码创建了一个 `String`:

```rust
let s = String::from("hello");
```

当创建这个 `String` 时, 程序向操作系统申请了一片内存. 但是如何把这片内存还给操作系统呢? 在有 *GC*
的编程语言中, 你不需要关心它; 没有 *GC* 的其它语言中, 需要手动释放这片内存, 这是很容易出问题的,
例如忘记释放, 过早释放, 多次释放等. 在 Rust 中, 是当这片内存离开作用域时自动释放的.

```rust
{
    let s = String::from("hello"); // s 在这之后是有效的

    // do stuff with s
}                                  // 该作用域结束了, s 不再有效
```

当变量离开作用域时, Rust 自动为我们调用了一个函数 `drop` 来释放相应的内存.


#### 变量和数据的交互方式: 移动

多个变量与同一个数据交互:

```rust
let s1 = String::from("hello");
let s2 = s1;
```

如果 `s2` 是 `s1` 的一个浅拷贝, 按照前面说的当变量离开作用域时将释放变量使用的内存, 则当 `s1` 和
`s2` 都离开作用域后, 同一片内存将被释放两次. 如果 `s2` 是 `s1` 的一个深拷贝, 则这种操作是比较费时的.
与其做深拷贝, Rust 认为 `s1` 不再有效, 所以当 `s1` 离开作用域时不会释放什么.
编译下面的代码将得到错误:

```rust
let s1 = String::from("hello");
let s2 = s1;

println!("{}", s1); // 这里将出错, s1 不再有效
```

`let s2 = s1;` 这条语句类似于浅拷贝, 但是它同时使得 `s1` 不再有效. 在 Rust 中我们把它叫做 `移动`,
即 `s1` 被移动到了 `s2`.


#### 变量和数据的交互方式: 克隆

如果确实需要复制 `String` 的堆上的数据, 你可以调用 `clone` 方法:

```rust
let s1 = String::from("hello");
let s2 = s1.clone();
// 这里 s1, s2 都是有效的
```


#### 栈上数据: 拷贝

下面的代码是有效的:

```rust
let x = 5;
let y = x;

println!("x: {}, y: {}", x, y);
```

这段代码似乎和我们刚才学到的有冲突: 我们没有调用 `clone`, 但是 `x` 仍然是有效的而且没有被移动到 `y`.

原因是像整数这样的类型, 它们的大小在编译时是已知的, 而且完全是存储在栈上的, 所以拷贝是很快的. Rust
有一个叫做 `Copy` trait 的特殊注解, 可以用在像整型这样的存储在栈上的类型上(后面会介绍 trait).
如果一个类型拥有 `Copy` trait, 将一个变量赋值给另一个变量后, 原来的变量还是有效的. Rust
不允许实现了 `Drop` trait 的类型拥有 `Copy` trait.

##### 哪些类型是 `Copy` 的?

* 整型, 例如 `i32`
* 布尔类型 `bool`
* 浮点类型, 例如 `f64`
* 字符类型 `char`
* 所有成员类型都是 `Copy` 的元组类型
* 成员类型是 `Copy` 的数组类型


### 所有权与函数

将值传递给函数的语义, 类似于将值赋值给变量. 此时值将被 `移动` 或 `拷贝`.

```rust
fn main() {
    let s = String::from("hello");  // s 进入作用域

    takes_ownership(s);             // s 的值被移动到函数
                                    // ... s 在这之后不再有效

    let x = 5;                      // x 进入作用域

    makes_copy(x);                  // x 被拷贝到函数
                                    // x 在这之后依然有效

} // 这里, x 离开作用域, 然后 s 也离开作用域. 因为 s 的值被移动了, 不会对 s 调用 drop

fn takes_ownership(some_string: String) { // some_string 进入作用域
    println!("{}", some_string);
} // 这里, some_string 离开作用域, 调用 drop. 使用的堆上的内存被释放.

fn makes_copy(some_integer: i32) { // some_integer 进入作用域
    println!("{}", some_integer);
} // 这里, some_integer 离开作用域. some_integer 的类型是 Copy 的, 不会调用 drop
```


### 返回值与作用域

函数返回值也会转移所有权.

```rust
fn main() {
    let s = gives_ownership();         // gives_ownership 的返回值被移动到 s
} // 这里 s 离开作用域, s 被 drop

fn gives_ownership() -> String {
    let some_string = String::from("hello"); // some_string 进入作用域

    some_string                              // some_string 被返回, 并被移动到调用函数
} // 这里 some_string 已被移动了, 不会调用 drop
```

如果我们想在调用一个函数后, 还能继续使用被移动到该函数的变量, 该怎么办呢?
一个方法是在这个函数中将该变量返回:

```rust
fn main() {
    let s = String::from("hello");
    let (s, len) = calculate_length(s); // 这里旧的且无效的变量 s 被隐藏了

    println!("s: {}, len: {}", s, len);
}

fn calculate_length(s: String) -> (String, usize) {
    let len = s.len();

    (s, len)
}
```

但是你不觉得这样很麻烦吗? 下节介绍 `引用`, 它将解决该问题.
