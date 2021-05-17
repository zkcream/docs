# zkCREAM docs

![github pages](https://github.com/zkcream/docs/workflows/github%20pages/badge.svg)

## Setup

This documentation is written in [mdbook](https://github.com/rust-lang/mdBook) format.

### Requirement

mdBook version has to be version `0.4.5` or later due to cross site scripting vulnerability. See [official report](https://blog.rust-lang.org/2021/01/04/mdbook-security-advisory.html) from rust website.

```bash
cargo install mdbook
```

If you already installed mdBook version `<= 0.4.4`, you need to upgrate to version 0.4.5 or later with following command.

```bash
cargo install mdbook --version 0.4.5 --force
```

## Build

```bash
mdbook build
```

## Contributions

Contributions are highly appreciated and encouraged. Don't hesitate to participate to discussions in the issues, propose new features and ask for help.

## License

All the code in this repository is released under the **GNU General Public License v3.0**, for more information take a look at the [LICENSE](./LICENSE) file.
