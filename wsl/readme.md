
https://gist.github.com/4wk-/889b26043f519259ab60386ca13ba91b
# how to re-install

## uninstall
```bash
# list all installed distros
wsl -l -v

# destroy distros
wsl --unregister Ubuntu
wsl --unregister Debian # and so on
```

## install
```bash
# install Ubuntu
# list available distributions
wsl --list --online

# install favorite distro
wsl --install -d Ubuntu-24.04

# set Debian as default
wsl --set-default Ubuntu-24.04
```