# fcli – Installation & Basic Usage

This document summarizes the most important steps and commands shown in the video on installing and using fcli.

## Table of Contents

1. [Installation and Enabling Auto Completion](#1-installation-and-enabling-auto-completion)
2. [How fcli Is Structured](#2-how-fcli-is-structured)
3. [Built-In Help](#3-built-in-help)
4. [Getting Started with the Config and Utility Modules](#4-getting-started-with-the-config-and-utility-modules)
5. [Listing All Commands](#5-listing-all-commands)
6. [Output Formats](#6-output-formats)
7. [Using the Query Feature](#7-using-the-query-feature)
8. [Working with Variables](#8-working-with-variables)
9. [Documentation](#9-documentation)
10. [Reporting Issues & GitHub](#10-reporting-issues--github)

## 1. Installation and Enabling Auto Completion

### 1.1 Visit the Repository
- Go to [GitHub.com/fortify/fcli](https://github.com/fortify/fcli).
- You will find Releases as well as online and offline documentation.

### 1.2 Download the Latest Release
- Download the latest release (e.g., native binaries for your OS or the `fcli.jar`).
- Additionally, you can download `.sha256` and `.rsa_sha256` files for integrity/signature verification.
- More information on automated integrity checks can be found in the fcli documentation.

### 1.3 Add fcli to Your PATH and Enable Auto Completion
Example for macOS (Zsh/Bash):
```bash
# Mac PATH setup
echo 'export PATH="/Users/janwienand/dev/fcli-mac:$PATH"' >> ~/.zshrc && source ~/.zshrc
echo $PATH

# Enable auto completion
echo 'source /Users/janwienand/dev/fcli-mac/fcli_completion' >> ~/.bash_profile && source ~/.bash_profile
source ~/.bash_profile
```

## 2. How fcli Is Structured
- `fcli -h`
- Displays all available modules (sub-commands).

Example:
```bash
fcli -h
```

## 3. Built-In Help

### General Help
- `fcli -h`
- Shows synopsis, description, options, and available sub-commands.

Example:
```bash
fcli -h
```

### Module-Specific Help
- `fcli [module-name] -h`
- Shows help for a specific module.

Example:
```bash
fcli ssc -h
```

- Each sub-command has its own help page:
```bash
fcli <module> <sub-command> -h
```

## 4. Getting Started with the Config and Utility Modules
- `fcli config -h`
  - Manages generic fcli configuration like proxy settings, trusted public keys, and the trust store.
- `fcli util -h`
  - Provides generic utility commands not tied to specific products.

## 5. Listing All Commands
- `fcli util all-commands -h`
  - Displays a list of all available fcli commands.
- Notable options: `--query`, `--output`, `--store`, `--log-level`, and `--log-file`.

Example:
```bash
fcli util all-commands ls
```

Notes:
- Hidden commands are internal and not intended for public use.
- Preview commands are functional but subject to change.

## 6. Output Formats
- `fcli util all-commands ls -o -h`
  - Displays all available output formats.
- `fcli util all-commands ls -o yaml`
  - Outputs in YAML format.
- `fcli util all-commands ls -o yaml --to-file=test.yaml`
  - Saves the YAML output to `test.yaml`.

## 7. Using the Query Feature
- `fcli util all-commands ls -o json`
  - JSON output helps see available properties for querying.
- `fcli util all-commands ls -q runnable`
  - Lists all runnable commands.
- `fcli util all-commands ls -q "runnable && module=='fod'"`
  - Lists only commands from the `fod` module that are runnable.

**Important:** Ensure to enclose the query in quotes as required by your shell.

## 8. Working with Variables
- `fcli util all-commands ls -q "runnable && module=='fod'" --store fod_commands`
  - Stores output in a variable called `fod_commands`.
- `fcli util variable ls`
  - Lists all stored variables.
- `fcli util variable contents fod_commands -o table=command`
  - Displays stored variable contents in table format.

Example Use Case:
- You can store a scan ID from `sast-scan start` and pass it to `sast-scan wait-for`.

## 9. Documentation
- Detailed documentation is available here:
  - [GitHub Repository](https://github.com/fortify/fcli)
  - Online docs at [fortify.github.io/fcli](https://fortify.github.io/fcli)
- Provides access to manual pages such as `fcli(1)`.

## 10. Reporting Issues & GitHub
- `fcli -V`
  - Outputs the current version of fcli.
- Always include the `fcli` version in your bug reports or enhancement requests.
- **Log File Options**:
  - Check via `fcli util all-commands list -h`.
- The fcli team prefers that bugs and enhancement requests be opened as an issue on GitHub.
- **Caution**: The GitHub Issues page is public. If you need to share confidential information, contact your OpenText representative.

**Happy fcli usage!** If you have any questions or ideas for improvements, feel free to reach out.
