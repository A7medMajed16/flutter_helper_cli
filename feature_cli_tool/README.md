# Feature CLI Tool

A command-line tool for creating a feature folder structure in Dart projects.

## Installation

To use this tool globally, you must make all scripts (`feature`, `add-dependencies`, `init-project`, etc.) executable and place them in your system's PATH.

For example, assuming you are in the root workspace directory with all the CLIs:
```bash
chmod +x feature_cli_tool/feature "dependency helper/add-firebase" "dependency helper/add-dependencies" "init project/init-project"
sudo cp feature_cli_tool/feature "dependency helper/add-firebase" "dependency helper/add-dependencies" "init project/init-project" /usr/local/bin/
```

## Usage

### Initialize a Project

Set up the clean architecture folder structure for your project:

```
feature initProject
```

You can also provide an optional custom core source path:

```
feature initProject /path/to/core
```

> **Note:** `init-project` also works as an alias for `initProject`.

### Create a Feature

Create a new feature folder structure by running:

```
feature create <feature_name>
```

Replace `<feature_name>` with the desired name of your feature (e.g., `splash`).

### Help

To see the usage information:

```
feature -h
```

## Commands Reference

| Command | Description |
|---|---|
| `feature initProject [path]` | Initializes the project with clean architecture structure. Optionally accepts a core source path. |
| `feature create <name>` | Creates a clean architecture feature folder structure for the given feature name. |
| `feature -h` / `feature --help` | Shows usage help. |

## Project Structure

The tool will create the following folder structure for the specified feature:

```
lib/
└── features/
    └── feature_name/
        ├── presentation/
        │   ├── bloc/
        │   ├── screens/
        │   │   └── feature_name_screen.dart
        │   └── widgets/
        ├── domain/
        │   ├── entities/
        │   ├── repositories/
        │   │   └── feature_name_repo.dart
        │   └── usecases/
        └── data/
            ├── models/
            ├── repositories/
            │   └── feature_name_repo_impl.dart
            └── datasources/
                ├── local_datasources/
                │   └── feature_name_local_datasources.dart
                └── remote_datasources/
                    └── feature_name_remote_datasources.dart
```

## Contributing

Feel free to submit issues or pull requests to improve the tool. Contributions are welcome!

## License

This project is licensed under the MIT License. See the LICENSE file for more details.