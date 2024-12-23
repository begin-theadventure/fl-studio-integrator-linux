# FL Studio Integrator
Integrate FL Studio with your Linux system.

[+](https://github.com/begin-theadventure/fl-studio-integrator-linux?tab=readme-ov-file#tips) tips and possible performance improvements.

#### So what does it do?
It doesn't take care of installing FL Studio, but integrating it with the system:

- Provides(/Installs) a shell script that runs the `.exe` with Wine and a `.desktop` application shortcut (/and an icon);

- Associates the `.flp` files and allows to open them (thanks [defusq](https://aur.archlinux.org/packages/vtfedit)) from the file manager, desktop etc., or the terminal: `fl-studio-integrator "/path/to/*.flp"`.

In version 1.0.4, two new integrations have been added for `.exe`, `.lnk`, `.msi` and `.reg` files! Making stuff such as updating (FL Studio, plugins), installing (plugins) or offline activating with a reg file easier.

## How to install
Arch - [the AUR](https://aur.archlinux.org/packages/fl-studio-integrator).

Different distros:

**<details><summary> Home (recommended)</summary>**

1. Download `Source Code` (from [releases](https://github.com/begin-theadventure/fl-studio-integrator-linux/releases/latest)) and the [icon](https://image-line.com/wp-content/themes/intracto/build/images/fl-header-logo.png) (as fl-studio.png).

2. Extract the file and move `.local` to the home directory `~`.

3. Go to `~/.local/share/applications`, make `fl-studio-integrator`, `-elm`, and `-reg` executable and edit the `WINEPREFIX` path in them.

4. Add `/home/`ReplaceThisWithYourUSERname in `fl-studio-integrator.desktop`, `-elm`, and `-reg` to `Exec=` and `Icon=` (before `/.local/`..).

6. Go to `~/.config` and add `application/flp=fl-studio-integrator.desktop;` in `mimeapps.list`.

To open from the terminal create alias commands:

`alias fl-studio-integrator='~/.local/share/applications/fl-studio-integrator'`

`alias fl-studio-integrator-elm='~/.local/share/applications/fl-studio-integrator-elm'`

`alias fl-studio-integrator-reg='~/.local/share/applications/fl-studio-integrator-reg'`

in one of these files (depending on your shell - most likely bash): `~/.bashrc` / `~/.zshrc` / `~/.config/fish/config.fish`.
</details>

**<details><summary> Root </summary>**
1. `Download snapshot` from [the AUR](https://aur.archlinux.org/packages/fl-studio-integrator) and the [icon](https://image-line.com/wp-content/themes/intracto/build/images/fl-header-logo.png) (as fl-studio.png).
2. Make `fl-studio-integrator`, `-elm`, and `-reg` executable and edit the `WINEPREFIX` path in them.
3. Place the files like in the [PKGBUILD](https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=fl-studio-integrator#n32) (lines 32-39, `/usr/`..).
4. `sudo update-mime-database /usr/share/mime` (for file associations).
</details>

#### Tips

**<details><summary> Plugin GUI glitches </summary>**
1. Running the plugin in a `Detached` mode; re-clicking `Captonize` or `Detailed settings` buttons; clicking on the plugin.
2. `export WINEDDLOVERRIDES="d2d1=disabled"`.
3. Installing DXVK and/or VKD3D (they can fix glitches in some, but also cause them in others, particularly DXVK).
4. Wine versions with the Vulkan child window patch ([more information](https://bugs.winehq.org/show_bug.cgi?id=45277)), such as: [wine-tkg](https://github.com/Frogging-Family/wine-tkg-git), [wine-ge-custom](https://github.com/GloriousEggroll/wine-ge-custom), [wine-lutris](https://github.com/lutris/wine).

</details>

**<details><summary> DXVK/VKD3D </summary>**
<details><summary> Winetricks (recommended)</summary>

In the terminal:
`cd` /path/to/prefix -> `winetricks dxvk vkd3d`

To update, add the `-f` (force) flag: `winetricks -f dxvk vkd3d`

Or with the GUI:

`cd` "/path/to/prefix" (in the terminal) -> `winetricks --gui` -> `Selected the default wineprefix` `OK` -> `Install a Windows DLL`.. `OK` -> `dxvk` `vkd3d` `OK`.
</details>

<details><summary> Manual </summary>

Symlink the prefix to `~/.wine`.

Download [DXVK](https://github.com/doitsujin/dxvk/releases/latest) and the [install script](https://github.com/doitsujin/dxvk/blob/4f90d7bf5f9ad785660507e0cb459a14dab5ac75/setup_dxvk.sh) -> `./setup_dxvk.sh install` in the terminal.

Download [VKD3D](https://github.com/HansKristian-Work/vkd3d-proton/releases/latest) -> `./setup_dxvk.sh install` in the terminal.

After installing you can delete the symlink.

To update, do the same steps; to uninstall, change `install` to `uninstall`."</details>
</details>

**<details><summary> Low latency </summary>**
[WineASIO](https://github.com/wineasio/wineasio), adjust with [`PIPEWIRE_QUANTUM`](https://github.com/PipeWire/pipewire#usage), which is already included in the scripts.
</details>

**<details><summary> Virtual desktop </summary>**
`wine` `explorer /desktop=FLStudio,RESOLxUTION`, for example, `1920x1080`.
</details>

**<details><summary> Wine Breeze Dark theme </summary>**
[Link](https://gist.github.com/Zeinok/ceaf6ff204792dde0ae31e0199d89398).

To install, open the file with `FL Studio REG` (or `fl-studio-integrator-reg` in the terminal).
</details>

**<details><summary> Disabling internet access in the prefix </summary>**
Wine Control Panel (`fl-studio-integrator-elm "/path/to/drive_c/windows/system32/control.exe"` or go to the path and open it with `FL Studio ELM`) -> Internet Settings -> Connections -> Use a proxy server ✓ - Type something random in Address and Port - Apply - OK
</details>

**<details><summary> How to use `export` enviroment variables? </summary>**
Paste them into the `fl-studio-integrator` script (and optionally `fl-studio-integrator-elm`).

One per line.
</details>

#### Possible performance improvements

**<details><summary> GameMode </summary>**
Add `gamemoderun` into the `fl-studio-integrator` script (and optionally `fl-studio-integrator-elm`) on the same line as `wine` (but before it): [`gamemoderun`](https://github.com/FeralInteractive/gamemode) `wine`.

* Renice

Adjusting the nice value/priority of processes in [/etc/gamemode.ini](https://github.com/FeralInteractive/gamemode/blob/master/example/gamemode.ini#L24), for example, to 7 (High).</summary>
</details>

**<details><summary> fsync </summary>**
Needs a patched Wine version, such as: [wine-tkg](https://github.com/Frogging-Family/wine-tkg-git), [wine-ge-custom](https://github.com/GloriousEggroll/wine-ge-custom), [wine-lutris](https://github.com/lutris/wine).
```
export WINEESYNC=0 WINEFSYNC=1
```

</details>

**<details><summary> NVIDIA </summary>**
These might cause issues.
```
export __GL_SHADER_DISK_CACHE_SKIP_CLEANUP=0 __VK_LAYER_NV_optimus="NVIDIA_only" VK_ICD_FILENAMES="/usr/share/vulkan/icd.d/nvidia_icd.json"
```

`__GLX_VENDOR_LIBRARY_NAME="nvidia"`, `__NV_PRIME_RENDER_OFFLOAD=1` and `prime-run` (can) cause crashes.
</details>

**DXVK/VKD3D might also help**.

### Of course, this project is in no way affiliated with the FL Studio developers.
