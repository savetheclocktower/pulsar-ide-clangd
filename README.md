# pulsar-ide-clangd

Provides C and C++ language support for [Pulsar] using [Clangd language server][Clangd].

## About this package

The `clangd` language server acts as a “brain” for lots of IDE features. This package knows how to feed that information to the packages that consume it.

Install this package, then install any of the following packages to get special features:

* [autocomplete-plus](https://web.pulsar-edit.dev/packages/autocomplete-plus) (builtin)
  * See autocompletion options as you type
* [symbols-view](https://web.pulsar-edit.dev/packages/symbols-view) (builtin)
  * View and filter a list of symbols in the current file
  * View and filter a list of symbols across all files in the project
  * Jump to the definition of the symbol under the cursor
* [linter](https://web.pulsar-edit.dev/packages/linter) and [linter-ui-default](https://web.pulsar-edit.dev/packages/linter-ui-default)
  * View diagnostic messages as you type
* [intentions](https://web.pulsar-edit.dev/packages/intentions)
  * Open a menu to view possible code actions for a diagnostic message
  * Open a menu to view possible code actions for the file at large
* [pulsar-refactor](https://web.pulsar-edit.dev/packages/pulsar-refactor)
  * Perform project-wide renaming of variables, methods, classes and types
* [pulsar-find-references](https://web.pulsar-edit.dev/packages/pulsar-find-references)
  * Place the cursor inside of a token to highlight other usages of that token
  * Place the cursor inside of a token, then view a `find-and-replace`-style “results” panel containing all usages of that token across your project
* [pulsar-outline-view](https://web.pulsar-edit.dev/packages/pulsar-outline-view)
  * View a hierarchical list of the file’s symbols
* [atom-ide-outline](https://web.pulsar-edit.dev/packages/atom-ide-outline)
  * View a hierarchical list of the file’s symbols
  * View the call hierarchy for a given file
* [atom-ide-datatip](https://web.pulsar-edit.dev/packages/atom-ide-datatip)
  * Hover over a symbol to see any related documentation, including method signatures
* [atom-ide-signature-help](https://web.pulsar-edit.dev/packages/atom-ide-signature-help)
  * View a function’s parameter signature as you type its arguments
* [atom-ide-code-format](https://web.pulsar-edit.dev/packages/atom-ide-code-format)
  * Invoke on a buffer (or a subset of your buffer) to reformat your code according to the language server’s settings
* [atom-ide-definitions](https://web.pulsar-edit.dev/packages/atom-ide-definitions)
  * Jump to the definition of the symbol under the cursor


All contributions and feedback are appreciated.

## Requirements

+ [Pulsar] 1.100 or later
+ [Clangd] executable installed in your path ([prebuilt binaries])

Autocompletion support via `autocomplete-plus` is built-in. If you’re running Pulsar 1.113 or later, so is symbol search via `symbols-view` — symbols within the document and the project, plus go-to-declaration functionality.

Other services can be consumed with various packages. You can install [atom-ide-base] for the maximal experience, but I’d encourage you to pick and choose a bit more carefully!

## Compilation Database

In order to make this plugin work effectively, clangd requires information about how your code should be compiled. There are two options: compile_commands.json, or compile_flags.txt.

### compile_commands.json

[CMake] is currently your best bet for generating a compile_commands.json file. The command to generate compile_commands.json along with your project looks something like this: `cmake (SOURCE_DIR) -DCMAKE_EXPORT_COMPILE_COMMANDS=ON`

CMake doesn't include header information in the compile_commands.json file. To rectify this, I use a tool called [compdb].

Clangd won't see your compile_commands.json file if it's placed in your build directory, so you should either symlink it to your project directory, or have compdb generate its output there.

### compile_flags.txt

[Another supported solution][compile-flags] is to make a compile_flags.txt file and place it in your project directory. Clangd will treat all project files with the same options. A simple compile_flags.txt might look something like this:

```
-std=c++11
-Iinclude
-DMY_DEBUG_FLAG
```

## Areas of interest

+ Automatic installation of Clangd

[Pulsar]: https://pulsar-edit.dev/
[Clangd]: https://clang.llvm.org/extra/clangd.html
[CMake]: https://cmake.org
[compdb]: https://github.com/Sarcasm/compdb
[compile-flags]: https://clang.llvm.org/docs/JSONCompilationDatabase.html#alternatives
[langserver]: http://langserver.org
[prebuilt binaries]: http://releases.llvm.org/download.html
[atom-ide-ui]: https://web.pulsar-edit.dev/packages/atom-ide-base
