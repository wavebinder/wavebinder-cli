# Wave Binder CLI

CLI tool designed to support **Wave Binder** development, aimed at simplifying the creation and maintenance of the JSON input file. The goal is to minimize manual errors and speed up the editing of even complex JSON structures.

The tool provides guided commands to add and modify nodes, with basic validation and interactive support when needed.

---

## Main features

* Dedicated CLI for managing Wave Binder JSON input
* Add new nodes with explicit type (MULTI, COMPLEX, LIST, SIMPLE)
* Edit existing nodes
* Interactive JSON file selection when not specified
* Clear output and immediate feedback on operations

---

## Requirements

* **Node.js** >= 18 recommended
* **npm**

The package is **not published on the npm registry**: installation is done via a local `.tgz` file.

---

## Installation

Given a local package `wave-binder-cli-<version>.tgz`:

```bash
npm install ./wave-binder-cli-0.0.1.tgz
```

This will make the binary available via `npx`.

> Alternatively, during local development, `npm link` can be used, but it is **not the recommended flow** for standard usage.

---

## Usage

The main command is `wbcli`.

Typical invocation:

```bash
npx wbcli <command> [options]
```

If the target JSON file is not specified, the CLI will interactively ask which file to operate on.

---

## Available commands

### `add`

Adds a new node to the JSON file.

```bash
npx wbcli add <nodeName> <nodeType> [options]
```

**Arguments**

* `nodeName` – name of the node to create
* `nodeType` – node type (`MULTI`, `COMPLEX`, `LIST`, `SIMPLE`)

**Options**

* `-f, --father <node>`
  Specifies the parent node under which the new node will be inserted

* `-j, --json <file>`
  Path to the target JSON file

**Example**

```bash
npx wbcli add tracks LIST -f root -j input.json
```

---

### `edit`

Edits an existing node in the JSON file.

```bash
npx wbcli edit <nodeName> [options]
```

**Arguments**

* `nodeName` – name of the node to edit

**Options**

* `-t, --type <nodeType>`
  Sets a new type for the node

* `-j, --json <file>`
  Path to the target JSON file

**Example**

```bash
npx wbcli edit tracks --type MULTI -j input.json
```

---

## Tool behavior

* If the JSON file is not passed via `--json`, the tool starts an interactive selection
* Changes are **written directly to the file**
* A summary of the operation result is printed after each command

---

## Project status

The project is in an **early stage** and intended for internal or controlled use. The CLI API and node format may evolve over time.

---

## License

All rights reserved by the Wave Binder owners.

---

## Development notes

* Based on `commander` for command parsing
* Interactive prompts implemented with `inquirer`
* Colored output via `chalk`
