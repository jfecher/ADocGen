# ADocGen

Generates markdown documentation for an Ante project from its doc comments.
This is currently restricted to Hugo pages for the [Ante website](https://antelang.org).

## Building

ADocGen must link with Ante's compiler, so build the compiler's C API first.
Note that this project currently expects the ante compiler must be located in `../ante`,
so your parent directory should look like:

```
./my-parent-dir
./my-parent-dir/ante
./my-parent-dir/ADocGen
```

```sh
# in ./ante
$ cargo build -p ante-capi --release
```

Then you can build ADocGen itself:

```sh
# in ./ADocGen
$ ante build
```

This will create a `ADocGen` executable in the current directory.

## Usage

```sh
./ADocGen [options] <project-directory> <output-directory>
```

`<project-directory>` is the directory containing the project's `src` directory.
Only the documentation for exported items is generated.

- `--stdout` prints every page instead of writing files
- `--strict` fails if any exported item lacks a doc comment
- `--title <text>` title of the index page (defaults to the crate's name)
- `--source-url <url>` base URL of the `src` directory, used to link each item to its source

Exported items without a doc comment are reported as warnings on stderr.
