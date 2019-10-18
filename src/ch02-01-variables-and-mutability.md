## 变量及可变性

变量默认是不可变的, 绑定一个值后, 不能再修改这个值.

```rust,ignore
let x = 5;
x = 6;
```

尝试编译上面的代码将得到一个错误:

    error[E0384]: cannot assign twice to immutable variable `x`
    --> src/main.rs:3:5
    |
    2 |     let x = 5;
    |         -
    |         |
    |         first assignment to `x`
    |         help: make this binding mutable: `mut x`
    3 |     x = 6;
    |     ^^^^^ cannot assign twice to immutable variable

要让变量可变, 需要在变量名前添加关键字 `mut`:

```rust
let mut x = 5;
println!("x: {}", x);
x = 6;
println!("x: {}", x);
```


### 变量与常量的区别

与不可变的变量相似, 常量是不能修改的. 和变量相比, 有如下区别:

* 使用关键字 `const` 声明, 且必须包含类型注解;

* 不允许使用 `mut`;

* 可以在任何作用域声明, 包括全局作用域;

* 只能使用常量表达式赋值.

例如:

```rust
const MAX_POINTS: u32 = 10_000;
```


### 隐藏

可以声明一个同名的新变量来隐藏一个变量, 被隐藏的旧变量将不可用.

```rust
let x = 5;
let x = x + 1;

let spaces = "   ";
let spaces = spaces.len();
```
