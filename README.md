# addToPath

This repository contains a script to add an "Add to PATH" option to the right-click context menu in Windows Explorer. This feature allows users to quickly add the path of a selected folder to the system's `PATH` environment variable without having to manually modify environment variables.

## Features

- Adds a context menu option for folders that allows adding their path to the system `PATH`.
- Integrates seamlessly into the Windows Explorer context menu.
- Provides an easy and convenient way to manage environment variables.

## How It Works

The script modifies the Windows Registry by adding new entries under `HKEY_CLASSES_ROOT\Directory\shell` and `HKEY_CLASSES_ROOT\Directory\Background\shell`. These entries create a context menu option called "Add to PATH" for directories.

When the option is clicked, a command is executed to append the selected folder's path to the system's `PATH` environment variable using the `setx` command.

## Installation

### Method 1: Using a `.reg` File

1. **Download the `.reg` File**: Download the `AddToPath.reg` file from this repository.
2. **Run the `.reg` File**:
   - Double-click the `AddToPath.reg` file.
   - Confirm any security prompts to add the entries to the Windows Registry.
3. **Restart Windows Explorer**:
   - For the changes to take effect, restart Windows Explorer or log out and back in.

### Manual Installation via Registry Editor

1. **Open Registry Editor**:
   - Press `Win + R`, type `regedit`, and press Enter.
2. **Navigate to**:
   - `HKEY_CLASSES_ROOT\Directory\shell`
3. **Create Keys**:
   - Create a new key called `AddToPath`.
   - Set the default value to `Add to PATH`.
   - Create a subkey called `command` under `AddToPath`.
   - Set the default value of the `command` key to:
     ```cmd
     cmd.exe /c "setx PATH \"%PATH%;%1\""
     ```
4. **Repeat**:
   - If desired, repeat the above steps for `HKEY_CLASSES_ROOT\Directory\Background\shell` to enable the context menu option when right-clicking on a blank space in a folder.

## Uninstallation

1. **Remove the Registry Entries**:
   - Open Registry Editor.
   - Navigate to `HKEY_CLASSES_ROOT\Directory\shell\AddToPath` and delete the `AddToPath` key.
   - Repeat for `HKEY_CLASSES_ROOT\Directory\Background\shell\AddToPath` (if applicable).
2. **Reboot** your system to remove the context menu option.

## Usage

After installation, simply:

1. **Right-click** on any folder in Windows Explorer.
2. Select the **"Add to PATH"** option from the context menu.
3. The folder's path will be added to the system's `PATH` environment variable.

## Important Notes

- **`setx` Command**: The script uses the `setx` command to permanently modify the `PATH` environment variable. Unlike the `set` command, `setx` changes persist across system restarts.
- **Character Limit**: The system `PATH` environment variable has a character limit. Continuously adding to it without managing the entries may eventually cause issues.
  
## License

This script is open-source and free to use under the MIT License.
