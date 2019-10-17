# 开始之前


## 入坑

本人不擅忽悠, 先请下面这些大神带你入坑吧:

* <a href="https://www.zhihu.com/question/30407715/answer/48032883" target="_blank">
    如何看待 Rust 的应用前景</a>

* <a href="https://www.infoq.cn/article/Uugi_eIJusEka1aSPmQM" target="_blank">
    想要改变世界的 Rust 语言</a>


## 安装

执行下面的命令开始安装 Rust:

```sh
curl https://sh.rustup.rs -sSf | sh
```

安装会修改 `~/.profile` 并把 Rust 添加到 `PATH` 中, 但是要等到下一次登录后才有效. 如果不想重启电脑,
可以执行下面的命令来手动把 Rust 添加到 `PATH`:

```sh
source ~/.cargo/env
```

如果在安装过程中遇到问题, 请前往 <a href="https://www.rust-lang.org/zh-CN/tools/install"
target="_blank">这里</a>. 安装之后你可以执行 `rustup update` 来更新 Rust, 或者执行 `rustup self
uninstall` 来卸载 Rust, 查看本地文档执行 `rustup doc`.


## Hello, World!

按照传统, 我们首先写一个打印 `Hello, World!` 的程序. 创建一个名为 *main.rs* 的文件, 你的目录结构看起
来可能像这样:

    codes/hello_world
    └── main.rs

Rust 文件始终使用 *.rs* 后缀; 如果文件名包含多个单词, 使用下划线分隔, 例如相比 *helloworld.rs*, 我们
更倾向于使用 *hello_world.rs*.

现在打开刚才创建的文件 *main.rs* 并输入以下代码:

```rust
fn main() {
    println!("Hello, world!");
}
```

上面的代码定义了一个名为 `main` 的无参数, 无返回值的函数. `fn` 是用来定义函数的关键字; 如果函数有参
数, 参数将写在括号中; 函数体包含在花括号中, 把左花括号放在函数声明的同一行是一个好的习惯; `println!`
是一个宏, Rust 的宏通常以 `!` 结尾.

同 C 一样, `main` 是一个特殊的函数名, 它是可执行程序的入口.

编译并运行:

```sh
rustc main.rs
./main
```

使用 `rustc` 来编译单个文件的项目是没问题的, 但是如果项目中包含多个文件, 这将非常麻烦. 接下来介绍
Cargo 工具, 它将帮助你编写真正的 Rust 程序.


## Hello, Cargo

Cargo 是 Rust 的构建系统和包管理器, 大多数 Rust 程序员使用这个工具来管理他们的项目. Cargo 可以做很多
工作, 比如构建你的代码, 下载依赖的库等等.


### 使用 Cargo 创建一个新的项目

```sh
cargo new hello_cargo
```

现在你的目录结构看起来应该像这样:

    codes/hello_cargo
    ├── Cargo.toml
    └── src
        └── main.rs

*Cargo.toml* 是一个 [TOML](https://github.com/toml-lang/toml) 格式的文件, 打开它:

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Huacheng Tan <huacheng.tan@foxmail.com>"]
edition = "2018"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```

`[package]` 表示接下来的配置是用来配置一个包(package)的, `[dependencies]` 下是项目的依赖(这里没有).

打开 *src/main.rs*:

```rust
fn main() {
    println!("Hello, world!");
}
```

这个文件和 [Hello, World!](# "Hello, World!") 部分的手动输入的 *main.rs* 一样.


### 构建和运行一个 Cargo 项目

进入 *hello_cargo* 目录并执行以下命令:

```sh
cargo build
./target/debug/hello_cargo
```

也可以把这两步结合起来:

```sh
cargo run
```

使用命令 `cargo check` 快速的检查代码是否可以编译, 但是不生成可执行文件; `cargo build --release` 构
建启用了优化的 Release 版本, 生成的可执行文件在 *target/release/* 中.
