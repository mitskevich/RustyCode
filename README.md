[![Build Status](https://travis-ci.org/saviorisdead/RustyCode.svg)](https://travis-ci.org/saviorisdead/RustyCode)

# Rust for Visual Studio Code (Latest: 0.19.1)

[Changelog](CHANGELOG.md)

[Roadmap](ROADMAP.md)

This extension adds advanced language support for the Rust language to VS Code, including:

- Autocompletion (using `racer`)
- Go To Definition (using `racer`)
- Go To Symbol (using `rustsym`)
- Format (using `rustfmt`)
- Linter *checkOnSave is experimental*
- Linting can be done via  *checkWith is experimental*
	- `check`. This is the default. Runs rust compiler but skips codegen pass.
	- `check-lib`. As above, but is limited only to library if project has library + multiple binaries
	- `clippy` if `cargo-clippy` is installed
	- `build`
- Cargo tasks (Open Command Pallete and they will be there)
- Snippets


### IDE Features
![IDE](images/ide_features.png)

## Using

First, you will need to install Visual Studio Code `1.0` or newer. In the command pallete (`cmd-shift-p`) select `Install Extension` and choose `RustyCode`.

Then, you need to install Racer (instructions and source code [here](https://github.com/phildawes/racer)). Please, note that we only support latest versions of `Racer`.

Also, you need to install Rustfmt (instructions and source code [here](https://github.com/rust-lang-nursery/rustfmt))

And last step is downloading Rust language source files from [here](https://github.com/rust-lang/rust).

### Options

The following Visual Studio Code settings are available for the RustyCode extension. These can be set in user preferences or workspace settings (`.vscode/settings.json`)

```javascript
{
	"rust.racerPath": null, // Specifies path to Racer binary if it's not in PATH
	"rust.rustLangSrcPath": null, // Specifies path to /src directory of local copy of Rust sources
	"rust.rustfmtPath": null, // Specifies path to Rustfmt binary if it's not in PATH
	"rust.rustsymPath": null, // Specifies path to Rustsym binary if it's not in PATH
	"rust.cargoPath": null, // Specifies path to Cargo binary if it's not in PATH
	"rust.cargoHomePath": null, // Path to Cargo home directory, mostly needed for racer. Needed only if using custom rust installation.
	"rust.cargoEnv": null, // Specifies custom variables to set when running cargo. Useful for crates which use env vars in their build.rs (like openssl-sys).
	"rust.formatOnSave": false, // Turn on/off autoformatting file on save (EXPERIMENTAL)
	"rust.checkOnSave": false, // Turn on/off `cargo check` project on save (EXPERIMENTAL)
	"rust.checkWith": "build", // Specifies the linter to use. (EXPERIMENTAL)
	"rust.errorMode": "plain-text-new", // Error mode, see below.
}
```

### Error mode

`rust.errorMode` configuration option specifies how to process error output of `cargo` commands.

- `json-cargo`

  Cargo is invoked with `--message-format=json` argument. This argument is supported since __rust nightly >= 2016-10-10__. This is the best method, since it does not require full recompilation of the project if `cargo build` is called outside of VS Code.

- `json-rustc`

  Cargo is invoked with `RUSTFLAGS=--error-format=json` environment variable. Supported since __rust 1.12.0__ and __rust nightly > 2016-08-08__. Will require full recompilation of the project if `cargo build` will be called in plain-text error format mode afterwards (e.g. in terminal).

- `plain-text-new`

  Plain-text error message output format. Used since __rust 1.12.0__.

- `plain-text-old`

  Pre __1.12.0__ error message output format.

## Building and Debugging the Extension

[Repository](https://github.com/saviorisdead/RustyCode)

You can set up a development enviroment for debugging the extension during extension development.

First make sure you do not have the extension installed in `~/.vscode/extensions`. Then clone the repo somewhere else on your machine, run `npm install` and open a development instance of Code.

```bash
rm -rf ~/.vscode/extensions/RustyCode
cd ~
git clone https://github.com/saviorisdead/RustyCode
cd RustyCode
npm install
npm run-script compile
code .
```

You can now go to the Debug viewlet and select `Launch Extension` then hit run (`F5`).
If you make edits in the extension `.ts` files, just reload (`cmd-r`) the `[Extension Development Host]` instance of Code to load in the new extension code.  The debugging instance will automatically reattach.

## License
[MIT](LICENSE)
