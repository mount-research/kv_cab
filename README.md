typedb
========
[![crates.io version](https://img.shields.io/crates/v/typedb.svg)](https://crates.io/crates/typedb)
[![Build status](https://travis-ci.org/mount-tech/typedb.svg?branch=master)](https://travis-ci.org/mount-tech/typedb)
[![Documentation](https://docs.rs/typedb/badge.svg)](https://docs.rs/typedb)

Simple persistent generic HashMap/Key-value store, using file locking to limit writing between threads.

This is in a beta state at the moment.

[Documentation](https://docs.rs/typedb)

Basic usage:
```rust
use typedb::{ KV, Value };

fn main() {
    let mut test_store = KV::<String, Value>::new("./db.cab");

    let _ = test_store.insert("key".to_string(), Value::String("value".to_string()));
    println!("{:?}", test_store.get("key".to_string()));
    let _ = test_store.remove("key".to_string());
}
```

Usage with user defined Key and Value types:
```rust
use typedb::{KV, key, value};
use serde_derive::{ Serialize, Deserialize };

key!(
enum MyKey {
    String(String),
    Int(i32),
});

value!(
enum MyValue {
    String(String),
    Int(i32),
});

fn main() {
    let mut test_store = KV::<MyKey, MyValue>::new("./db.cab").unwrap();

    let _ = test_store.insert(MyKey::Int(1i32), MyValue::String("value".to_string()));
    println!("{:?}", test_store.get(MyKey::Int(1i32)));
    let _ = test_store.remove(MyKey::Int(1i32));
}
```

[License](https://github.com/mount-tech/typedb/blob/master/LICENSE.md)
