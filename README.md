# FL Studio Linux Integrator
Integrate FL Studio with your Linux system.

(_If you're on Arch use [the AUR version](https://aur.archlinux.org/packages/fl-studio-integrator)_) 

(_If you're using a different distro check out the [releases](https://github.com/begin-theadventure/fl-studio-integrator-linux/releases/latest)_)

#### So what does it do?
It doesn't take care of installing FL Studio, but of integrating it with your system:

- Provides a shell script (*you need specify the Wine prefix path in it*) that runs the `.exe` with Wine, a `.desktop` application shortcut and the icon;

- Associates the `.flp` files and allows to open them (thanks [defusq](https://aur.archlinux.org/packages/vtfedit)) from the file manager, desktop etc., or the terminal: `fl-studio-integrator "/path/to/*.flp"`.
