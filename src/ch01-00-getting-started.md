# 开始


## 先入坑

本人不擅忽悠, 先让下面这位大神们带你入坑吧:

- <a href="https://www.infoq.cn/article/Uugi_eIJusEka1aSPmQM" target="_blank">
    想要改变世界的 Rust 语言</a>


## 安装

执行下面的命令开始安装 Rust:

```sh
curl https://sh.rustup.rs -sSf | sh
```

安装会修改 `~/.profile` 把 Rust 添加到 `PATH` 中, 但是要等到下一次登录后才有效. 如果不想重启电脑, 可
以执行下面的命令来手动把 Rust 添加到 `PATH`:

```sh
source ~/.cargo/env
```


## 实用命令

    rustup update         : 更新 Rust
    rustup self uninstall : 卸载 Rust
    rustup doc            : 查看本地文档
