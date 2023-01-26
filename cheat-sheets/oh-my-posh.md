# Oh My Posh

**Oh My Posh** is a custom prompt engine for any shell that has the ability to adjust the prompt string with a function or variable.

## Install

1. Install **Oh My Posh**

    ```powershell
    winget install JanDeDobbeleer.OhMyPosh -s winget
    ```

2. Install **Meslo** fonts

    ```powershell
    oh-my-posh font install
    ```

    Prompt require admin rights. Fonts will be installed for all users.

    If there is any error You can download latest version from [here](https://github.com/ryanoasis/nerd-fonts/releases) and install it manually.

3. Add **Oh My Posh** to PowerShell

    1. Open PowerShell profile script

        ```powershell
        notepad $PROFILE
        ```

        If there is an error create profile file

        ```powershell
        New-Item -Path $PROFILE -Type File -Force
        ```

    2. Add the following line

        ```powershell
        oh-my-posh init pwsh | Invoke-Expression
        ```

    3. Save file and reload PowerShell

        ```powershell
        . $PROFILE
        ```

## Customize

To add custom fields, modify colors etc. add config path in profile script

```powershell
oh-my-posh init pwsh --config '<path to config file>' | Invoke-Expression
```
