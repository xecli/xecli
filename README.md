<p align="center">
  <img src="Assets/xecli-wordmark.png" alt="XeCLI logo" width="360">
</p>

<p align="center">
  A Windows command-line and desktop toolkit for Xbox 360 RGH/JTAG development, diagnostics, file management, and reverse-engineering workflows.
</p>

<p align="center">
  <a href="https://github.com/xecli/xecli/releases">Downloads</a> ·
  <a href="https://github.com/xecli/xecli/wiki">Documentation</a> ·
  <a href="SUPPORT.md">Support</a> ·
  <a href="SECURITY.md">Security</a>
</p>

Use `rgh.exe` for direct commands and automation, or open `XeTerminal.exe` for the connected desktop workspace. Both applications are included in every v2.0.0 package.

<p align="center">
  <img src="Assets/readme/xeterminal-v2.png" alt="XeTerminal showing four of 19 themes: Cyan, Amber, Violet, and Ruby" width="1200">
</p>

## Install

Download XeCLI only from the official [GitHub Releases](https://github.com/xecli/xecli/releases) page. Both packages are self-contained for x64 Windows and do not require a separate .NET installation. Windows 11 is recommended; see [Requirements](#requirements) for supported Windows 10 editions.

| Package | Choose it for | System behavior |
| --- | --- | --- |
| **Installer**: `XeCLI-2.0.0-win-x64-setup.exe` | A standard installed experience | Creates the XeCLI Start menu entry automatically. XeCLI desktop shortcut creation and adding `rgh` to `PATH` are optional. Installed-mode state uses Windows profile folders by default. |
| **Portable ZIP**: `XeCLI-2.0.0-win-x64.zip` | A movable or self-contained folder | Extract and run `rgh.exe` or `XeTerminal.exe`. It performs no installation or `PATH` changes and stores state under the package-local `UserData` folder by default. |

The installer defaults to `%LOCALAPPDATA%\Programs\XeCLI` for the current user or `%ProgramFiles%\XeCLI` for all users; either location can be changed in setup.

> **Unsigned release:** XeCLI v2.0.0 is intentionally unsigned. Windows may display **Unknown Publisher** or a SmartScreen warning. Verify the matching `.sha256` file from the Releases page before running either package.

```powershell
Get-FileHash .\XeCLI-2.0.0-win-x64-setup.exe -Algorithm SHA256
Get-Content .\XeCLI-2.0.0-win-x64-setup.exe.sha256

Get-FileHash .\XeCLI-2.0.0-win-x64.zip -Algorithm SHA256
Get-Content .\XeCLI-2.0.0-win-x64.zip.sha256
```

The hash printed by `Get-FileHash` must match the first value in its downloaded checksum file.

## Quick Start

After enabling the installer `PATH` option, close any terminal that was already open before setup and open a new one before running:

```powershell
rgh health
rgh start
rgh status
```

`rgh start` discovers a console and saves it as the default target. If discovery is unavailable, set the target directly with `rgh connect <console-ip>`. If you skipped `PATH` registration, run `rgh.exe` from the installation directory you selected. In the portable package, use `.\rgh.exe` instead of `rgh`; launch `.\XeTerminal.exe` for the desktop interface.

## Commands

XeCLI has 62 root commands, grouped into console connection, power and launch, live debugging, hardware control, FTP and content, local packages and storage, XeLL, Ghidra and IDA integration, and reporting. Run `rgh <command> --help` for built-in help, or see the [Commands Reference](https://github.com/xecli/xecli/wiki/Commands) and the full [CLI Help Output](https://github.com/xecli/xecli/wiki/CLI-Help).

What changed in v2.0.0 is in [UPDATES.md](UPDATES.md) and the [release notes](https://github.com/xecli/xecli/releases).

## Requirements

- x64 Windows 11 is recommended. On Windows 10, Microsoft supports .NET 10 only on eligible Enterprise and LTSC releases (21H2, 1809, and 1607); the installer requires build 14393 or later. See the current [.NET support matrix](https://learn.microsoft.com/dotnet/core/install/windows#supported-versions).
- An Xbox 360 RGH/JTAG console with a compatible XBDM plugin for live console commands
- JRPC2 only for command families that use its RPC transport
- A compatible dashboard or DashLaunch FTP service for FTP workflows
- A local Ghidra or IDA installation only for the corresponding optional integrations

Run `rgh ftp check` when XBDM works but FTP does not. Run `rgh health` for local configuration, saved-target/profile, and command-log checks without connecting to a console.

## Documentation

Start with the [Beginner Guide](https://github.com/xecli/xecli/wiki/Beginner-Guide), then use the [Commands Reference](https://github.com/xecli/xecli/wiki/Commands) for task-oriented examples or [CLI Help Output](https://github.com/xecli/xecli/wiki/CLI-Help) for the complete built-in command surface.

Focused guides cover [FTP requirements and file transfer](https://github.com/xecli/xecli/wiki/FTP-and-File-Transfer), [reverse engineering](https://github.com/xecli/xecli/wiki/Reverse-Engineering), [XeLL workflows](https://github.com/xecli/xecli/wiki/XeCLI-XellFetch), [FATX/XTAF](https://github.com/xecli/xecli/wiki/FATX-Manager), and [troubleshooting](https://github.com/xecli/xecli/wiki/Troubleshooting).

## Data and Uninstall

Installed mode stores configuration under `%APPDATA%\XeCLI`, cache and the default command log under `%LOCALAPPDATA%\XeCLI`, and default XeTerminal captures under the Windows Pictures folder at `XeCLI\Captures`. Configured capture or log directories remain where you selected them. Upgrades preserve user settings, and uninstall leaves all of these user-owned locations untouched; remove them manually only when no longer needed.

Portable mode keeps configuration, cache, logs, and default captures under `UserData` beside the executables. Moving the complete extracted folder moves that state with it. In either mode, `XECLI_HOME` overrides the default state roots and stores configuration, cache, logs, and default captures in the directory it names.

## Support, Security, and Contributing

- Read [SUPPORT.md](SUPPORT.md) before opening a [GitHub issue](https://github.com/xecli/xecli/issues).
- Report security concerns through the private process described in [SECURITY.md](SECURITY.md); never place secrets or sensitive console files in a public issue.
- Contributions are welcome under [CONTRIBUTING.md](CONTRIBUTING.md).
- If XeCLI saves you time, you can support development on [Ko-fi](https://ko-fi.com/xecli).

XeCLI is licensed under the [GNU General Public License v3.0](LICENSE). Dependency and bundled-component provenance is documented in [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).
