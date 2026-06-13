# Terminal Configs

These are my terminal larp configs, using [Fashfetch](https://github.com/fastfetch-cli/fastfetch).

![Preview image of the terminal](./readme/preview.png)

## Setup
First, download Fastfetch and clone the repository.
1. Open PowerShell, not Command Prompt.
2. Download Fastfetch
```
winget install Fastfetch-cli.Fastfetch
```
3. Generate the config directories and files.
```
fastfetch --gen-config
```
4. Go to the Fastfetch config folder
```
cd $env:USERPROFILE/.config/fastfetch
```
5. Ensure that the file is empty. 
> [!CAUTION]
> **YOU MUST ENSURE THAT YOU ARE IN THE CORRECT DIRECTORY. THIS CANNOT BE UNDONE.** You should
check manually if you can.
```
Remove-Item * -Recurse -Force
```
You can also tick the `-WhatIf` flag to check.
```
Remove-Item * -Recurse -Force -WhatIf
```
6. Clone this repository into the fastfetch config folder.
```
git clone https://github.com/Faizaan-J/terminal-configs.git .
```
---
Now we will have Windows Command Prompt and PowerShell run `fastfetch` on start.

7. Check if a PowerShell profile is present.
```
Test-Path $PROFILE
```
If not, run
```
New-Item -Type File -Path $PROFILE -Force
```
8. Edit the profile `.ps1` file and place in the following at the end:
```
fastfetch
```
9. Create a file named `init.cmd` anywhere. Place the following inside of it:
```
@echo off
fastfetch
```
10. Run this command to create a `AutoRun` registry entry that runs `init.cmd` everytime Command Prompt opens. Make sure to replace `[YOUR_TARGET_PATH_HERE]`.
```
reg add "HKCU\Software\Microsoft\Command Processor" /v AutoRun /t REG_EXPAND_SZ /d "%[YOUR_TARGET_PATH_HERE]%\init.cmd" /f
```
---
Lastly, we will apply a custom color scheme to the Windows Terminal and create a symbolic link so that it links the `settings.json` from this repository to the location that Windows Terminal stores the settings.

11. Depending on whether you are running the Standard or Preview release of Windows Terminal, delete `settings.json`.

Stable:
```
Remove-Item "$env:LOCALAPPDATA\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\settings.json" -Force
```

Preview:
```
Remove-Item "$env:LOCALAPPDATA\Packages\Microsoft.WindowsTerminalPreview_8wekyb3d8bbwe\LocalState\settings.json" -Force
```
12. Open PowerShell again except `Run As Administrator`.
13. Create a symbolic link between the repository and the location of Windows Terminal settings, still corresponding to whether you are using the Stable or Preview release of Windows Terminal.

Stable:
```
New-Item -ItemType SymbolicLink -Path "$env:LOCALAPPDATA\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\settings.json" -Value "$env:USERPROFILE\.config\fastfetch\settings.json" -Force
```

Preview:
```
New-Item -ItemType SymbolicLink -Path "$env:LOCALAPPDATA\Packages\Microsoft.WindowsTerminalPreview_8wekyb3d8bbwe\LocalState\settings.json" -Value "$env:USERPROFILE\.config\fastfetch\settings.json" -Force
```

---
It should be configured now! Make sure it works by opening another terminal window. It should automatically run `fastfetch` on the startup of both PowerShell and Command Prompt.

## Credits
- Windows Terminal Themes for the [Retrowave](https://windowsterminalthemes.dev/?theme=Retrowave) theme.

<a href="https://github.com/atomcorp/themes">
  <img src="./readme/GithubLogo.png" alt="Github logo. Links lead to atomcorp/themes repository." width="35">
</a>

---

- [asciiart.eu/image-to-ascii](https://www.asciiart.eu/image-to-ascii) for helping to convert images to ASCII art.
