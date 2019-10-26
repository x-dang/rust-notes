## 定义结构体

```rust
// 定义结构体
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}

fn main() {
    // 实例化结构体:
    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    // 使用 . 操作符访问结构体的成员
    println!("email: {}", user1.email);

    // 结构体更新语法(..instance): 从已有实例创建一个新的实例
    let mut user2 = User {
        username: String::from("anotherusername567"),
        email: String::from("another@example.com"),
        ..user1 // 注意, 结尾不能有逗号. 该语法表示其余成员的值与 user1 对应的值相同
    };

    // 修改结构体成员. 如果想要成员可变, 必须整个实例都是可变的, 不能单独标注某个成员是可变的
    user2.email = String::from("anotheremail@example.com");
}

// 成员初始化语法: 如果用于初始化结构体成员的变量名与成员名相同, 可以只写成员名
fn build_user(email: String, username: String) -> User {
    User {
        email, // 你也可以写成: "email: email,", 但是 "email," 更简洁
        username,
        active: true,
        sign_in_count: 1,
    }
}
```


### 元组结构体

成员没有名字, 可以使用类似访问元组成员的方式访问成员.

```rust
struct Color(u8, u8, u8);

let red = Color(255, 0, 0);

println!("r: {}, g: {}, b: {}", red.0, red.1, red.2);
```


### 类单元结构体(Unit-Like Structs)

`struct Foo();` 定义了一个没有任何成员的类单元结构体 `Foo`. 这种结构体在你只想为一个新的类型实现
trait, 但是不包含任何成员时比较有用.


### 调试

可以在结构体定义前加一行 `#[derive(Debug)]`, 这样就可以在 `println!` 中使用 `{:?}` 或 `{:#?}`
占位符来打印结构体内容了:

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect = Rectangle { width: 30, height: 50, };

    println!("rect is {:?}", rect);
    println!("rect is {:#?}", rect);
}
```
