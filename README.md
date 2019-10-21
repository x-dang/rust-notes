# Rust 简明教程

[目录](src/SUMMARY.md)

---

本书主要参考 "the book" ([*The Rust Programming Language*](https://github.com/rust-lang/book.git)).
因为 "the book" 的内容太过于详细, 一个简单的知识点却花费了大量篇幅. 这对于初学者来说也许是好的,
但对于有经验的, 或仅因某概念记不清想快速找回记忆的人来说, "the book" 读起来太费时了.

本书的首要目的是简明, 如果因为本书太过简明以至于看不懂, 请参考 "the book" 的对应章节.


## 构建

本书使用 [mdBook](https://github.com/rust-lang-nursery/mdBook) 构建, 使用下面的命令安装它:

```sh
cargo install mdbook
```

构建本书:

```sh
mdbook build
```

然后在浏览器中打开 *book/index.html* 即可开始阅读.
