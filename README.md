# Duso Sublime Text Package

Language Server Protocol (LSP) support for Duso in Sublime Text.

> **⚠️ Requires Duso Installation**
>
> The LSP features (error diagnostics, hover documentation, go to definition, find references) require the `duso` binary to be installed on your system. Visit [duso.rocks](https://duso.rocks) for installation instructions.

## Features

- **Syntax Highlighting** - Color coded syntax for Duso scripts
- **Error Diagnostics** - Real-time parse error detection
- **Hover Documentation** - View built-in function documentation
- **Go to Definition** - Jump to function and variable definitions
- **Find References** - Find all usages of variables and functions

## Installation

1. Install the **LSP** package from Package Control (if not already installed)
2. Install this package via Package Control: `Duso`
3. Restart Sublime Text

## Prerequisites

Ensure the `duso` binary is in your PATH:

```bash
which duso
duso --version
```

If duso is not found, the extension will fail to start. Make sure you've run `./build.sh` in the project root.

## Quick Test

1. Create a file `test.du`:
   ```duso
   print("Hello, Duso!")

   function greet(name) do
     print("Hello, " + name)
   end

   greet("World")
   ```

2. Open the file in Sublime - you should see syntax highlighting

3. Hover over `print` and `greet` to see documentation

4. Create a syntax error to see diagnostics:
   ```duso
   print(1 2)  # Missing comma
   ```

## Features

### Error Diagnostics
- Syntax errors shown in real-time with red squiggles
- Error details in the Problems panel

### Hover Documentation
- Hover over built-in functions (print, len, map, etc.) to see docs
- Shows function signatures and descriptions

### Go to Definition
- Click on a function/variable to jump to its definition
- Works for same-file definitions

### Find References
- Right-click → Find All References to find all usages
- Highlights all matching identifiers

## Architecture

The package launches `duso -lsp` which:
1. Reads LSP messages from Sublime over stdin
2. Parses documents and analyzes them
3. Sends diagnostics, hover info, and definitions back to Sublime

No separate server needed - it's built into the duso binary!

## Troubleshooting

If the server doesn't start:
1. Check View → Output Console for error messages
2. Verify `duso` is in PATH: `which duso`
3. Rebuild: `./build.sh` in project root
4. Restart Sublime: Cmd+Q then reopen
