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
uninstall` 来卸载 Rust, 查看本地文档请执行 `rustup doc`.
