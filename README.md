# 🛠️ Flutter Helper CLI

A collection of interactive Bash CLI tools to **supercharge your Flutter development workflow**. Automate project setup, feature scaffolding, dependency management, and release builds — all from one unified command.

```
flutter-helper
```

```
╔══════════════════════════════════════════════╗
║      Flutter Helper CLI v1.0.2              ║
╚══════════════════════════════════════════════╝
Select a tool to run (Up/Down to move, Enter to confirm):
> Init Project
  Create Feature
  Add Dependency
  Add Firebase Dependency
  Build Release
```

---

## 📦 Installation

### 1. Clone the repository

```bash
git clone https://github.com/A7medMajed16/flutter_helper_cli.git
cd flutter_helper_cli
```

### 2. Install globally

Copy all scripts to `/usr/local/bin/` so they're available system-wide:

```bash
sudo cp flutter-helper /usr/local/bin/
sudo cp "dependency helper/add-firebase" /usr/local/bin/
sudo cp "dependency helper/add-dependencies" /usr/local/bin/
sudo cp feature_cli_tool/feature /usr/local/bin/
sudo cp "init project/init-project" /usr/local/bin/
sudo cp flutter_release_cli/flutter-release /usr/local/bin/
```

### 3. Make sure they're executable

```bash
sudo chmod +x /usr/local/bin/flutter-helper
sudo chmod +x /usr/local/bin/add-firebase
sudo chmod +x /usr/local/bin/add-dependencies
sudo chmod +x /usr/local/bin/feature
sudo chmod +x /usr/local/bin/init-project
sudo chmod +x /usr/local/bin/flutter-release
```

### 4. Verify installation

```bash
flutter-helper -v
# flutter-helper version 1.0.2
```

---

## 🚀 Tools Overview

### 1. `flutter-helper` — Central Launcher

The main entry point. Run it from any Flutter project directory to access all tools through an interactive arrow-key menu.

```bash
flutter-helper
```

| Flag | Description |
|------|-------------|
| `-v`, `--version` | Print version |

---

### 2. `feature` — Clean Architecture Scaffolding

Generates a complete Clean Architecture feature folder structure with all the necessary boilerplate files.

#### Create a Feature

```bash
feature create <feature_name>
```

Creates the following structure under `lib/features/<feature_name>/`:

```
├── presentation/
│   ├── bloc/
│   ├── screens/
│   │   └── <feature_name>_screen.dart   # Pre-configured with @RoutePage()
│   └── widgets/
├── domain/
│   ├── entities/
│   ├── repositories/
│   ├── params/
│   │   └── <feature_name>_repo.dart
│   └── usecases/
└── data/
    ├── models/
    ├── repositories/
    │   └── <feature_name>_repo_impl.dart
    └── datasources/
        ├── local_datasources/
        │   └── <feature_name>_local_datasources.dart
        └── remote_datasources/
            └── <feature_name>_remote_datasources.dart
```

After creating the feature, it automatically runs `build_runner` to generate route files.

#### Initialize a Project

```bash
feature initProject [/path/to/core]
```

Sets up a new Flutter project with your core architecture template:
1. Runs the `add-dependencies` interactive selector
2. Copies your reusable `core/` folder into the project
3. Copies main app files and YAML configurations
4. Appends `flutter_launcher_icons` configuration to `pubspec.yaml`

---

### 3. `add-dependencies` — Interactive Dependency Manager

A TUI (Terminal UI) multi-select menu for adding popular Flutter packages. Packages are organized by category and toggled with the spacebar.

```bash
add-dependencies
```

**Categories included:**
| Category | Packages |
|----------|----------|
| Architecture & State Management | `bloc`, `flutter_bloc`, `get_it`, `injectable`, `build_runner`, `injectable_generator` |
| Networking & Data | `dio`, `pretty_dio_logger`, `shared_preferences`, `flutter_secure_storage` |
| Navigation & Routing | `auto_route`, `auto_route_generator` |
| UI & Assets | `cached_network_image`, `flutter_screenutil`, `flutter_svg`, `shimmer`, `toastification`, `lottie`, and more |
| Media & Files | `image_picker`, `image_cropper`, `file_picker`, `video_player`, `chewie`, `just_audio` |
| Utilities & Platform | `dartz`, `equatable`, `easy_localization`, `permission_handler`, `url_launcher`, and more |
| Environment & Tooling | `flutter_dotenv`, `flutter_launcher_icons`, `flutter_native_splash`, and more |

> **Note:** Dev dependencies (like `build_runner`, `auto_route_generator`) are automatically added with `--dev`.

**Controls:**
- `↑` `↓` — Navigate
- `Space` — Toggle selection
- `Enter` — Confirm and install

---

### 4. `add-firebase` — Firebase Package Selector

Same interactive TUI, specifically for Firebase packages.

```bash
add-firebase
```

**Categories included:**
| Category | Packages |
|----------|----------|
| Core | `firebase_core` |
| Authentication | `firebase_auth`, `firebase_app_check`, `firebase_ui_auth`, OAuth providers |
| Database & Storage | `cloud_firestore`, `firebase_database`, `firebase_storage` |
| Messaging & Analytics | `firebase_messaging`, `firebase_analytics`, `firebase_in_app_messaging` |
| Performance & Quality | `firebase_crashlytics`, `firebase_performance`, `firebase_remote_config` |
| Functions & Utilities | `cloud_functions`, `firebase_dynamic_links`, and more |

---

### 5. `flutter-release` — Automated Release Builder

Builds, versions, and optionally sends your APK/AAB to a Telegram group — all in one command.

```bash
flutter-release          # Build split APKs
flutter-release --aab    # Build AAB for Play Store
```

**What it does:**
1. **Reads** current version from `pubspec.yaml`
2. **Prompts** for change type (bug fix, UI, feature, or combination)
3. **Bumps** the version automatically:
   - 🐛 Bug fix → **patch** +1
   - 🎨 UI change → **minor** +1
   - ✨ New feature → **major** +1
   - 🔄 Rebuild → no version change
4. **Builds** release APK (split-per-abi) or AAB
5. **Sends** the build to your Telegram group via bot
6. **Cleans** up build artifacts
7. **Optionally commits** the version bump to git

#### Telegram Setup

On first run, a config file is created at `~/.flutter-release.env`:

```bash
TELEGRAM_BOT_TOKEN=your_bot_token_here
TELEGRAM_CHAT_ID=your_chat_id_here
```

Get your bot token from [@BotFather](https://t.me/BotFather) and your chat ID from [@userinfobot](https://t.me/userinfobot).

---

## 🖥️ Terminal Compatibility

The interactive menus (`add-dependencies`, `add-firebase`) use the **alternate screen buffer** for clean rendering. This means:
- ✅ Works in **any terminal size** (full-screen or small IDE panel)
- ✅ The list **dynamically adapts** to your terminal height
- ✅ **Scroll indicators** (`↑` `↓`) show when there are more items
- ✅ Original terminal content is **restored** when you exit

---

## 📋 Requirements

- **macOS** or **Linux**
- **Bash** 4.0+
- **Flutter** SDK installed and in `PATH`
- **Dart** SDK (comes with Flutter)

---

## 📁 Project Structure

```
flutter_helper_cli/
├── flutter-helper                       # Central launcher
├── feature_cli_tool/
│   └── feature                          # Feature scaffolding tool
├── dependency helper/
│   ├── add-dependencies                 # Flutter package selector
│   └── add-firebase                     # Firebase package selector
├── init project/
│   └── init-project                     # Project initializer
├── flutter_release_cli/
│   └── flutter-release                  # Release builder & Telegram sender
└── README.md
```

---

## 📄 License

This project is open source and available for personal and commercial use.

---

Made with ❤️ by [Ahmed Majed](https://github.com/A7medMajed16)
