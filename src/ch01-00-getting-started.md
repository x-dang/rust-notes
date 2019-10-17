# 开始之前


## 入坑

本人不擅忽悠, 先请下面这位大神带你入坑吧:

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

按照传统, 我们首先用 Rust 来写一个打印 `Hello, World!` 的程序. 创建一个名为 *main.rs* 的文件, 你的目
录结构可能看起来像这样:

    codes
    └── hello_world
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
