kv_cab
========

Simple persistent generic HashMap/Key-value store.

Simpple usage:
```rust
extern crate kv_cab;

use kv_cab::{ KV, Value };

fn main() {
    let mut test_store = KV::<String, Value>::new("./db.cab");

    let _ = test_store.insert("key".to_string(), Value::String("value".to_string()));
    println!("{:?}", test_store.get("key".to_string()));
    let _ = test_store.remove("key".to_string());
}
```

Usage with user defined Key and Value types:
```rust
extern crate kv_cab;
extern crate rustc_serialize;

use kv_cab::KV;

#[derive(Clone, RustcEncodable, RustcDecodable, PartialEq, Eq, Hash)]
enum MyKey {
    String(String),
    Int(i32),
}

#[derive(Clone, RustcEncodable, RustcDecodable, Debug)]
enum MyValue {
    String(String),
    Int(i32),
}

fn main() {
    let cab_path = "./db.cab";
    let mut test_store = KV::<MyKey, MyValue>::new(cab_path);

    let _ = test_store.insert(MyKey::Int(1i32), MyValue::String("value".to_string()));
    println!("{:?}", test_store.get(MyKey::Int(1i32)));
    let _ = test_store.remove(MyKey::Int(1i32));


    let _ = std::fs::remove_file(cab_path);
}
```
