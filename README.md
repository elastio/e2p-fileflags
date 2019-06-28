# e2p-fileflags:

[![Build Status](https://travis-ci.com/michaellass/e2p-fileflags.svg?branch=master)](https://travis-ci.com/michaellass/e2p-fileflags)
[![License: MIT](https://img.shields.io/crates/l/e2p-fileflags.svg](https://github.com/michaellass/e2p-fileflags/blob/master/LICENSE)
[![Version](https://img.shields.io/crates/v/e2p-fileflags.svg](https://crates.io/crates/e2p-fileflags)

e2p-fileflags provides access to file flags on Linux. Which flags exist,
depends on the file system used. This crate uses libe2p in the background,
which originates from e2fsprogs and supports flags for ext2, ext3, ext4,
xfs, f2fs and btrfs file systems.

## Examples
```rust
use std::fs::File;
use e2p_fileflags::{FileFlags,Flags};

let f = File::create("./foo/bar.txt").unwrap();
f.set_flags(Flags::NOCOW).unwrap();
println!("Flags: {:?}", f.flags());
```

```rust
use std::path::Path;
use e2p_fileflags::{FileFlags,Flags};

let p = Path::new("./foo/bar.txt");
p.set_flags(Flags::NOCOW).unwrap();
println!("Flags: {:?}", p.flags());
```

## Requirements
* libe2p, including development headers. Right now, libe2p in version 1.42.4 is
  required. If you need support for older versions, please open an issue and
  state the required version.

  Linux distributions typically packages those under one of the following names:
  * e2fsprogs(-dev)
  * e2fslibs(-dev)

  Note that after an update of libe2p, you may need to rebuild libe2p-sys and
  this crate to get access to any newly introduced flags.
