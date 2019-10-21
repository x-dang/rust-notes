## 控制流


### `if` 表达式

条件表达式的值必须是 `bool` 类型的.

```rust
fn main() {
    let number = 3;

    if number < 5 {
        println!("The number is less than 5.");
    }

    if number % 2 == 1 {
        println!("The number is odd.");
    } else {
        println!("The number is even.");
    }

    if number % 4 == 0 {
        println!("The number is divisible by 4.");
    } else if number % 3 == 0 {
        println!("The number is divisible by 3.");
    }
}
```


### 在 `let` 语句中使用 `if`

`if` 是一个表达式, 可以使用它来为变量赋值:

```rust
let condition = false;

let number = if condition {
    5
} else {
    6
};

println!("The number is {}", number);
```


### 循环

Rust 有三种循环: `loop`, `while`, `for`.


#### `loop` 循环

```rust
loop {
    println!("again!");
}
```


##### 从 `loop` 返回值

```rust
let mut counter = 0;

let x = loop {
    counter += 1;

    if counter == 10 {
        break counter * 2;
    }
};

println!("x: {}", x);
```


#### `while` 循环

```rust
let mut number = 3;

while number > 0 {
    println!("{}!", number);

    number -= 1;
}

println!("LIFTOFF!");
```


#### `for` 循环

```rust
let a = [1, 2, 3, 4, 5];

for element in a.iter() {
    println!("the value is: {}", element);
}


for number in (1..5).rev() {
    println!("number: {}", number);
}
```
