<!-- DO NOT REMOVE - contributor_list:data:start:["Matt-Gleich", "cjdenio", "safinsingh", "imgbot[bot]"]:end -->

<div align="center">
  <img alt="logo" src="./images/Entire%20Logo.png" height="250px">

  <h1>fgh</h1>

  <img alt="GitHub release (latest by date)" src="https://img.shields.io/github/v/release/Matt-Gleich/fgh">
  <img alt="GitHub go.mod Go version" src="https://img.shields.io/github/go-mod/go-version/Matt-Gleich/fgh">
  <img alt="Golang report card" src ="https://goreportcard.com/badge/github.com/Matt-Gleich/fgh">
  <br>
  <img alt="build" src="https://github.com/Matt-Gleich/fgh/workflows/build/badge.svg" />
  <img alt="test" src="https://github.com/Matt-Gleich/fgh/workflows/test/badge.svg" />
  <img alt="lint" src="https://github.com/Matt-Gleich/fgh/workflows/lint/badge.svg" />
  <img alt="release" src="https://github.com/Matt-Gleich/fgh/workflows/release/badge.svg" />
  <br />
  <br />
  <i>📁 Automate the organization of your cloned GitHub repositories</i>
</div>

<hr />

## 📜 Table of Contents

- [📜 Table of Contents](#-table-of-contents)
- [❓ What is `fgh`](#-what-is-fgh)
- [📟 Commands](#-commands)
  - [🔒 `fgh login`](#-fgh-login)
  - [⚙️ `fgh configure`](#️-fgh-configure)
  - [☁️ `fgh clone`](#️-fgh-clone)
    - [🔠 Keywords](#-keywords)
  - [⬆️ `fgh update`](#️-fgh-update)
  - [🧼 `fgh clean`](#-fgh-clean)
  - [🗑 `fgh remove`](#-fgh-remove)
  - [🧭 `fgh ls`](#-fgh-ls)
- [💡 Tips](#-tips)
  - [<owner/name> shorthand](#ownername-shorthand)
  - [`fgh ls` for `cd`](#fgh-ls-for-cd)
- [🗂 Custom Structures](#-custom-structures)
  - [📁 `structure_root`](#-structure_root)
  - [🗂 `structure`](#-structure)
  - [💡 Example](#-example)
- [🚀 Install](#-install)
  - [🍎 macOS](#-macos)
  - [🐧 Linux and 🖥 Windows](#-linux-and--windows)
- [🛣 Roadmap](#-roadmap)
- [🙌 Contributing](#-contributing)
- [👥 Contributors](#-contributors)

## ❓ What is `fgh`

As you begin contributing to an increasing amount of GitHub repositories, you'll soon realize the effort it takes to clone and organize them on your machine. `fgh` aims to solve this issue through the use of a CLI (command line application) to manage this entire process, saving you time _and_ helping you scale!

<!-- <details> -->
## 📟 Commands

### 🔒 `fgh login`

Before using `fgh`, you'll need to give it access to your GitHub account. Simply run `fgh login` to quickly get set up!

If you need to use a GitHub custom access token, like a PAT, edit the secret configuration file. On Windows it is located in `~/.fgh/secrets.yml` and `~/.config/fgh/secrets.yml` on Linux and Darwin (macOS) systems. You should change/add the `pat` as seen below:

```yaml
pat: <your token here>
```

### ⚙️ `fgh configure`

To configure other settings, run `fgh configure` for an interactive configuration experience.

### ☁️ `fgh clone`

To begin using `fgh`, you'll need to clone a repository, which you can do by running the following in a terminal window:

```bash
fgh clone <owner/name>
```

**OR**

```bash
fgh clone <name> # if the repo is under your account
```

All repositories are cloned into the following structure by default:

```
~
└─ github
   └─ OWNER
      └─ TYPE
         └─ MAIN_LANGUAGE
            └─ NAME
```

#### 🔠 Keywords

These names correspond to the following **keywords**:

- `OWNER` is the owner of the repository
- `TYPE` is the type of the repository; one of the following:
  - `public`
  - `private`
  - `template`
  - `archived`
  - `disabled`
  - `mirror`
  - `fork`
- `MAIN_LANGUAGE` is The main language that the repository contains. If no language is detected, `fgh` will just set it to `Other`
- `NAME` is the name of the repository

If you would like to use a custom structure see the [custom structures documentation](#-custom-structures). Usage of this command is as follows:

```bash
fgh clone <owner/name>
```

Would clone to `~/github/Matt-Gleich/public/Go/fgh/` by default, `~` being `$HOME`. Once cloned, this path will be copied to your clipboard automatically (this can be turned off with [`fgh configure`](#️-fgh-configure) or just by editing the config file directly).

> NOTE: On Linux machines running the X Window System, this program requires the `xclip` or `xsel` packages.

This structure can be somewhat difficult to navigate in the terminal using conventional methods such as the use of the `cd` command. I suggest TUI-based filesystem navigators such as [ranger](https://github.com/ranger/ranger) to help speed up the process.

### ⬆️ `fgh update`

If any of a repository's fields are changed, such as its type, main language, owner, or name, the path to your local repository won't match.

Running `fgh update` will iterate over your local repositories and checks if any of them need updates. If they do, `fgh` will ask you if you want to move the entire repository to that new path.

For example: If I had this repository cloned and later decided to archive it, its path would change from `~/github/Matt-Gleich/public/Go/fgh/` to `~/github/Matt-Gleich/archived/Go/fgh/`.

### 🧼 `fgh clean`

When you run this subcommand, `fgh` will check for the following on each repository:

1. Has it modified locally in a certain amount of time?
   > By default, this "amount of time" is 2 months. However, it can be changed with a flag! See `fgh clean --help` for more info.
2. Has the repository been deleted permanently on GitHub?

If either of those conditions are met, `fgh` will ask you if you would like to remove the aforementioned repository. It'll additionally show you some information about the repository itself.

> NOTE: This only removes the repo locally!

### 🗑 `fgh remove`

Remove a selected cloned repository. Usage is as follows:

```bash
fgh remove <owner/name>
```

### 🧭 `fgh ls`

Get the path of a cloned repository. Usage is as follows:

```bash
fgh ls <owner/name>
```

## 💡 Tips

### <owner/name> shorthand

Any command that takes `<owner/name>` as an argument allows you to leave off the `owner` if the repo is under your account. For example, I own this repo so I can just do

```bash
fgh clone fgh
```

instead of

```bash
fgh clone Matt-Gleich/fgh
```

### `fgh ls` for `cd`

If you would like to easily use the output of `fgh ls <owner/name>` for `cd` just add the following snippet to your `~/.zshrc` or `~/.bashrc`:

```bash
# cd with fgh (https://github.com/Matt-Gleich/fgh)
function fcd() { cd $(fgh ls "$@") }
```

Once you add that and reload your terminal you can simply run `fcd <owner/name>` instead of `fgh ls <owner/name>`, copying the output to your clipboard, typing `cd`, and pasting the output. Much easier!

## 🗂 Custom Structures

Not a fan of the default structure used by fgh? Don't worry, you can change it without losing any of fgh's automation. Configuring custom structures takes place in the general configuration file. This file is located in `~/.config/fgh/config.yaml` on Linux or macOS and `~\.fgh\config.yaml` on Windows (`~` is your home directory). There are two parts to creating custom structures:

### 📁 `structure_root`

This is where the structure starts relative to your home folder. Make sure you use `\` if you are on Windows. By default, the `structure_root` is `github`. Below is an example of what you would put in the general config file:

```yaml
structure_root: 'Documents/code/'
```

If we were to run `fgh clone Matt-Gleich/fgh` with just the config shown above it would be cloned to `~/Documents/code/Matt-Gleich/public/Go/fgh`

### 🗂 `structure`

This is the structure used inside of the [`structure_root`](#-structure_root) If you use the [keywords shown in the clone structure](#-keywords) it will automatically be replaced by the value for the repo. Below is an example of what you would put in the general config file:

```yaml
structure:
  - OWNER
  - repos
  - LANGUAGE
```

If we were to run `fgh clone Matt-Gleich/fgh` with just the config shown above it would be cloned to `~/github/Matt-Gleich/repos/Go/fgh`.

### 💡 Example

Say we have the following config:

```yaml
structure: 'code'
structure:
  - OWNER
```

If we were to run `fgh clone Matt-Gleich/fgh` it would clone the repo to `~/code/Matt-Gleich/fgh`.

## 🚀 Install

### 🍎 macOS

```bash
brew tap Matt-Gleich/homebrew-taps
brew install fgh
```

### 🐧 Linux and 🖥 Windows

You can grab the binary from the [latest release](https://github.com/Matt-Gleich/fgh/releases/latest).

## 🛣 Roadmap

- Add `pull` subcommand to pull the latest changes for each repository

## 🙌 Contributing

Thank you for considering contributing to `fgh`! Before contributing, make sure to read the [CONTRIBUTING.md file](https://github.com/Matt-Gleich/fgh/blob/master/CONTRIBUTING.md).

<!-- DO NOT REMOVE - contributor_list:start -->
## 👥 Contributors


- **[@Matt-Gleich](https://github.com/Matt-Gleich)**

- **[@cjdenio](https://github.com/cjdenio)**

- **[@safinsingh](https://github.com/safinsingh)**

- **[@imgbot[bot]](https://github.com/apps/imgbot)**

<!-- DO NOT REMOVE - contributor_list:end -->
