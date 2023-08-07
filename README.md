# FL Studio Integrator
Integrate FL Studio with your Linux system.

#### So what does it do?
It doesn't take care of installing FL Studio, but of integrating it with the system:

- Provides(/Installs) a shell script that runs the `.exe` with Wine and a `.desktop` application shortcut (/and an icon);

- Associates the `.flp` files and allows to open them (thanks [defusq](https://aur.archlinux.org/packages/vtfedit)) from the file manager, desktop etc., or the terminal: `fl-studio-integrator "/path/to/*.flp"`.

#### How to install
Arch - [the AUR](https://aur.archlinux.org/packages/fl-studio-integrator).

Different distros:
##### Home
<sup>(e.g. Steam Deck)</sup>

1. Download `fl-studio-integrator.zip` (from the [releases](https://github.com/begin-theadventure/fl-studio-integrator-linux/releases/latest)) and the [icon](https://image-line.com/wp-content/themes/intracto/build/images/fl-header-logo.png) (as fl-studio.png).

2. Extract the zip file in the home directory.

3. Go to `~/.local/share/applications`, make `fl-studio-integrator` executable and edit the `WINEPREFIX` path in it.

4. Add `/home/ReplaceThisWithYourUSERname` (before /..) in `fl-studio-integrator.desktop` to `Exec=` and `Icon=`.

6. Go to `~/.config` and add `application/flp=fl-studio-integrator.desktop;` to `mimeapps.list`.

To open from the terminal create an alias command:

`~/.bashrc` / `~/.zshrc` / `~/.config/fish/config.fish`: `alias fl-studio-integrator='~/.local/share/applications/fl-studio-integrator'`

##### Root
1. `Download snapshot` from [the AUR](https://aur.archlinux.org/packages/fl-studio-integrator) and the [icon](https://image-line.com/wp-content/themes/intracto/build/images/fl-header-logo.png) (as fl-studio.png).
2. Make `fl-studio-integrator` executable and edit the `WINEPREFIX` path in it.
3. Place the files like in the [PKGBUILD](https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=fl-studio-integrator#n22) (lines 22-25, `/usr/`..).

## Of course, this is not official.
