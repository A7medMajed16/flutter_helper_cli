# Add Firebase CLI

A standalone interactive CLI tool to select and install Firebase packages into your Flutter projects using a simple Terminal User Interface (TUI). 

## Installation

Make the script executable and copy it to your global path:

```bash
chmod +x add-firebase
sudo cp add-firebase /usr/local/bin/
```

## Usage

Simply run the command from the root of your Flutter project:

```bash
add-firebase
```

### Controls
- **Up/Down Arrows**: Move the cursor
- **Space**: Select/Unselect a package
- **Enter**: Confirm selection and auto-install via `flutter pub add`
