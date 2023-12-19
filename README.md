# FL Studio Integrator
Integrate FL Studio with your Linux system.

#### So what does it do?
It doesn't take care of installing FL Studio, but integrating it with the system:

- Provides(/Installs) a shell script that runs the `.exe` with Wine and a `.desktop` application shortcut (/and an icon);

- Associates the `.flp` files and allows to open them (thanks [defusq](https://aur.archlinux.org/packages/vtfedit)) from the file manager, desktop etc., or the terminal: `fl-studio-integrator "/path/to/*.flp"`.

In version 1.0.4, a new integration has been added for `.exe`, `.lnk`, `.msi` and `.reg` files!

#### How to install
Arch - [the AUR](https://aur.archlinux.org/packages/fl-studio-integrator).

Different distros:
##### Home

1. Download `fl-studio-integrator.zip` (from [releases](https://github.com/begin-theadventure/fl-studio-integrator-linux/releases/latest)) and the [icon](https://image-line.com/wp-content/themes/intracto/build/images/fl-header-logo.png) (as fl-studio.png).

2. Extract the zip file in the home directory.

3. Go to `~/.local/share/applications`, make `fl-studio-integrator`, `-elm`, and `-reg` executable and edit the `WINEPREFIX` path in them.

4. Add `/home/ReplaceThisWithYourUSERname` in `fl-studio-integrator.desktop`, `-elm`, and `-reg` to `Exec=` and `Icon=` (before `/.local/`..).

6. Go to `~/.config` and add `application/flp=fl-studio-integrator.desktop;` in `mimeapps.list`.

To open from the terminal create alias commands:

`~/.bashrc` / `~/.zshrc` / `~/.config/fish/config.fish`:

`alias fl-studio-integrator='~/.local/share/applications/fl-studio-integrator'`

`alias fl-studio-integrator-elm='~/.local/share/applications/fl-studio-integrator-elm'`

`alias fl-studio-integrator-reg='~/.local/share/applications/fl-studio-integrator-reg'`

##### Root
1. `Download snapshot` from [the AUR](https://aur.archlinux.org/packages/fl-studio-integrator) and the [icon](https://image-line.com/wp-content/themes/intracto/build/images/fl-header-logo.png) (as fl-studio.png).
2. Make `fl-studio-integrator`, `-elm`, and `-reg` executable and edit the `WINEPREFIX` path in them.
3. Place the files like in the [PKGBUILD](https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=fl-studio-integrator#n32) (lines 32-39, `/usr/`..).
4. `sudo update-mime-database /usr/share/mime` (for `.flp` association).

#### Tips

**<details><summary> Plugin GUI glitches </summary>**
`export WINEDDLOVERRIDES="d2d1=disabled"` might help.

As well as installing DXVK and/or VKD3D (they can fix glitches in some, but also cause them in others, particularly DXVK).
</details>

**<details><summary> DXVK/VKD3D </summary>**
Symlink the prefix to `~/.wine`.

Download [DXVK](https://github.com/doitsujin/dxvk/releases/latest) and the [install script](https://github.com/doitsujin/dxvk/blob/4f90d7bf5f9ad785660507e0cb459a14dab5ac75/setup_dxvk.sh) -> `./setup_dxvk.sh install` in the terminal.

Download [VKD3D](https://github.com/HansKristian-Work/vkd3d-proton/releases/latest) -> `./setup_dxvk.sh install` in the terminal.

After installing you can delete the symlink.

To update, do the same steps; to uninstall, change `install` to `uninstall`."
</details>

**<details><summary> Low latency </summary>**
[WineASIO](https://github.com/wineasio/wineasio), adjust with [`PIPEWIRE_QUANTUM`](https://github.com/PipeWire/pipewire#usage), which is already included in the script.
</details>

**<details><summary> Virtual desktop </summary>**
`wine` `explorer /desktop=FLStudio,RESOLxUTION`, for example, `1920x1080`.
</details>

**<details><summary> Wine Breeze Dark theme </summary>**
[Link](https://gist.github.com/Zeinok/ceaf6ff204792dde0ae31e0199d89398).

To install, open the file with `FL Studio REG` (or `fl-studio-integrator-reg` in the terminal).
</details>

**<details><summary> Disabling internet access in the prefix </summary>**

Wine Control Panel (`fl-studio-integrator-elm "/path/to/drive_c/windows/system32/control.exe"` or go to the path and open it with `FL Studio ELM`)-> Internet Settings -> Connections -> Use a proxy server ✓ - Type something in Address and Port - Apply - OK
</details>

#### Possible performance improvements

**<details><summary> GameMode </summary>**
[`gamemoderun`](https://github.com/FeralInteractive/gamemode) `wine`

* Renice

Adjusting the nice value/priority of processes, for example, to 7 (High).</summary>

[/etc/gamemode.ini](https://github.com/FeralInteractive/gamemode/blob/master/example/gamemode.ini)

```
[general]
; GameMode can renice game processes. You can put any value between 0 and 20 here, the value
; will be negated and applied as a nice value (0 means no change). Defaults to 0.
; To use this feature, the user must be added to the gamemode group (and then rebooted):
; sudo usermod -aG gamemode $(whoami)
renice=7
```
</details>

**<details><summary> esync / fsync </summary>**
```
export WINEESYNC=1 WINEFSYNC=1
```
</details>

**<details><summary> NVIDIA </summary>**
These might cause issues.
```
export __NV_PRIME_RENDER_OFFLOAD=1 __VK_LAYER_NV_optimus="NVIDIA_only" __GL_SHADER_DISK_CACHE_SKIP_CLEANUP=0
```

`prime-run` and `__GLX_VENDOR_LIBRARY_NAME="nvidia"` (can) cause crashes.
</details>

**DXVK/VKD3D might also help**.

# Of course, this project is not official.
