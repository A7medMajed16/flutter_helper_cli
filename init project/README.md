# Init Project CLI

A standalone script to initialize a structured Clean Architecture workspace in a Flutter project by copying core folders and YAML files.

## Installation

Make the script executable and copy it to your global path:

```bash
chmod +x init-project
sudo cp init-project /usr/local/bin/
```

## Usage

You can call this individually or via the `feature initProject` command (which orchestrates both dependency addition and project initialization).

```bash
init-project /path/to/core
```
