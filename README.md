# FL Studio Integrator
Integrate FL Studio with your Linux system.

#### So what does it do?
It doesn't take care of installing FL Studio, but integrating it with the system:

- Provides(/Installs) a shell script that runs the `.exe` with Wine and a `.desktop` application shortcut (/and an icon);

- Associates the `.flp` files and allows to open them (thanks [defusq](https://aur.archlinux.org/packages/vtfedit)) from the file manager, desktop etc., or the terminal: `fl-studio-integrator "/path/to/*.flp"`.

#### How to install
Arch - [the AUR](https://aur.archlinux.org/packages/fl-studio-integrator).

Different distros:
##### Home

1. Download `fl-studio-integrator.zip` (from [releases](https://github.com/begin-theadventure/fl-studio-integrator-linux/releases/latest)) and the [icon](https://image-line.com/wp-content/themes/intracto/build/images/fl-header-logo.png) (as fl-studio.png).

2. Extract the zip file in the home directory.

3. Go to `~/.local/share/applications`, make `fl-studio-integrator` executable and edit the `WINEPREFIX` path in it.

4. Add `/home/ReplaceThisWithYourUSERname` in `fl-studio-integrator.desktop` to `Exec=` and `Icon=` (before `/.local/`..).

6. Go to `~/.config` and add `application/flp=fl-studio-integrator.desktop;` in `mimeapps.list`.

To open from the terminal create an alias command:

`~/.bashrc` / `~/.zshrc` / `~/.config/fish/config.fish`: `alias fl-studio-integrator='~/.local/share/applications/fl-studio-integrator'`

##### Root
1. `Download snapshot` from [the AUR](https://aur.archlinux.org/packages/fl-studio-integrator) and the [icon](https://image-line.com/wp-content/themes/intracto/build/images/fl-header-logo.png) (as fl-studio.png).
2. Make `fl-studio-integrator` executable and edit the `WINEPREFIX` path in it.
3. Place the files like in the [PKGBUILD](https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=fl-studio-integrator#n22) (lines 22-25, `/usr/`..).

#### Tips, and possible performance improvements

**<details><summary> Plugin GUI glitches </summary>**
`export WINEDDLOVERRIDES="d2d1=disabled"`
</details>

**<details><summary> Low latency </summary>**
[WineASIO](https://github.com/wineasio/wineasio), adjust with `PIPEWIRE_QUANTUM`, which is already included in the script.
</details>

**<details><summary> Virtual desktop </summary>**
`wine` `explorer /desktop=FLStudio,RESOLxUTION`, for example, `1920x1080`.
</details>

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
export __NV_PRIME_RENDER_OFFLOAD=1 __VK_LAYER_NV_optimus="NVIDIA_only" VK_ICD_FILENAMES="/usr/share/vulkan/icd.d/nvidia_icd.json" __GL_SHADER_DISK_CACHE_SKIP_CLEANUP=0
```

`prime-run` and `__GLX_VENDOR_LIBRARY_NAME="nvidia"` cause crashes.
</details>

# Of course, this is not official.
