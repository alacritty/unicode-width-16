# unicode-width-16

**This crate is a fork** of https://github.com/unicode-rs/unicode-width with
Unicode 16 support and removed `normalization`.

Determine displayed width of `char` and `str` types according to
[Unicode Standard Annex #11][UAX11] rules.

[UAX11]: http://www.unicode.org/reports/tr11/

```rust
use unicode_width_16::UnicodeWidthStr;

fn main() {
    let teststr = "Ｈｅｌｌｏ, ｗｏｒｌｄ!";
    let width = UnicodeWidthStr::width(teststr);
    println!("{}", teststr);
    println!("The above string is {} columns wide.", width);
    let width = teststr.width_cjk();
    println!("The above string is {} columns wide (CJK).", width);
}
```

**NOTE:** The computed width values may not match the actual rendered column
width. For example, the woman scientist emoji comprises of a woman emoji, a
zero-width joiner and a microscope emoji.

```rust
use unicode_width_16::UnicodeWidthStr;

fn main() {
    assert_eq!(UnicodeWidthStr::width("👩"), 2); // Woman
    assert_eq!(UnicodeWidthStr::width("🔬"), 2); // Microscope
    assert_eq!(UnicodeWidthStr::width("👩‍🔬"), 4); // Woman scientist
}
```

See [Unicode Standard Annex #11][UAX11] for precise details on what is and isn't
covered by this crate.

## features

unicode-width does not depend on libstd, so it can be used in crates
with the `#![no_std]` attribute.

## crates.io

You can use this package in your project by adding the following
to your `Cargo.toml`:

```toml
[dependencies]
unicode-width-16 = "0.1.0"
```
