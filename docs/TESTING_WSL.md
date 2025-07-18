# Testing the Extension from WSL

This guide explains how you can build and try the extension directly on Windows while running the test binaries in WSL (Windows Subsystem for Linux).

## 1. Requirements

- A working installation of WSL with your preferred Linux distribution
- Node.js and npm installed in Windows
- Visual Studio Code with the Remote - WSL extension
- Your Google Test binary compiled for your target architecture
- (Optional) QEMU installed in WSL if you want to run the tests through QEMU

## 2. Build the Extension

1. Clone this repository under your Windows filesystem or inside WSL.
2. Install the dependencies by running `npm install` inside the repository directory.
3. Build the extension with `npm run build`.
4. Package it using `npm run package` which will create a `.vsix` file.

## 3. Install the Extension in VS Code

1. In Visual Studio Code, open the command palette and choose `Extensions: Install from VSIX...`.
2. Select the `.vsix` file produced in the previous step.
3. Reload VS Code when prompted.

## 4. Configure the Extension

Open (or create) `.vscode/settings.json` in your workspace and set at least the following options:

```json
{
    "gtestExplorer.executable": "path/to/your/test/executable",
    "gtestExplorer.cwd": "${workspaceFolder}",
    "gtestExplorer.useQemu": false
}
```

To run tests inside QEMU you can enable `useQemu` and customize `qemuPath` and `qemuArgs` if needed.

## 5. Running from WSL

Open the workspace in VS Code using the Remote - WSL extension so that VS Code runs in the Linux environment. The extension will then spawn your test executable (optionally through QEMU) directly within WSL.

Use the Test Explorer view to load and run your tests.

## 6. Troubleshooting

- Ensure that the executable path is correct relative to the workspace folder.
- Check the Output panel for any error messages from the adapter.
- If QEMU fails to start, verify the path and arguments in your settings.

