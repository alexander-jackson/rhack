# rhack
Would you like to quickly put a sneaky `dbg!` macro into external crates to find out how some internal data structure works? If so `rhack` is for you!

`rhack` makes it easier to edit external crates code that your project depends on.

## Usage

Let's say you want to modify the `reqwest` crate.

```toml
[dependencies]
reqwest = "0.11"
```

Run the following:

```
$ rhack edit reqwest
```

This will make a copy of the crate into `$HOME/.rhack/reqwest-0.11.1` and add its path to the [[patch] section](https://doc.rust-lang.org/edition-guide/rust-2018/cargo-and-crates-io/replacing-dependencies-with-patch.html) in your Cargo.toml:

```toml
[patch.'https://github.com/nakabonne/rhack']
reqwest = { path = "/home/you/.rhack/reqwest-0.11.1" }
```

Now your package uses the locally checked out copy instead of one from crates.io. You can now put the `dbg!` macro or edit it as you like!

### Undoing

```
$ rhack undo reqwest
```

### Settings
It uses `$HOME/.rhack` as the destination to copy the source code of the external crates by default. You can change it by setting and exposing the `$RHACK_DIR` environment variable.

## Inspired by
- [gohack](https://github.com/rogpeppe/gohack)
