# pacman recap

Install
-------
`pacman -S {pkg}` install {pkg}

`pacman -Syu` update package database and upgrade installed packages

`pacman -Ss <name>` search package by <name> on remote repo 

`pacman -Sy` update package database

`pacman -Su` upgrade installed packages

`pacman -Syy` force update of package database even if recently updated

`pacman -Syyuw` download programs but leave them uninstalled (for manual install)

`pacman -Si <name>` info remote package

Remove
------

`pacman -R {pkg}` remove package {pkg}

`pacman -Rs` remove package as well as unneeded dependencies

`pacman -Rns` remove package, dependencies, and system config files (recommended for all package uninstallations)

Query local repo
----------------

`pacman -Q` display all installed packages

`pacman -Qi {pkg}` display packages detail

`pacman -Q | wc -l` display total number of installed packages by counting lines of output

`pacman -Qe` display only packages explicitly installed

`pacman -Qeq` display only names of explicitly installed packages, and not version numbers ("quiet")

`pacman -Qn` display only packages installed from main repositories

`pacman -Qm` display only packages installed from AUR

`pacman -Qdt` display orphaned dependencies

`pacman -Ss` search remote repository for package

`pacman -Qs` search local repository for package


Aur
----------------

`git clone <repository>`

`makepkg -si` 
  
Basic Maintenance
----------------  
  
```
# clean cache
sudo pacman -Sc 
yay -Sc
  
# list orphan package
sudo pacman -Qdtq  

# remove all orphan package
sudo pacman -Rns $(pacman -Qdtq)
````
