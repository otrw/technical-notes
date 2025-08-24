# DNF Cheatsheet

Small collection of commands and options relating to using `dnf` package manager.

```bash
# Search & info
dnf se <term>                  # search
dnf info <pkg>                 # package details
dnf repoquery --whatprovides <file-or-virt>   # who provides X?
dnf repolist                   # enabled repos
dnf repoinfo                   # details
dnf needs-restarting           # check if reboot required

# Install / remove
sudo dnf in <pkg1> <pkg2>      # install
sudo dnf rm <pkg>              # remove
sudo dnf reinstall <pkg>       # reinstall
sudo dnf upgrade --refresh     # full upgrade

# Groups / environments
dnf group list                 # list groups
sudo dnf group install "Development Tools"
sudo dnf group remove "<Group>"

# History (roll back a bad transaction)
dnf history                    # show transactions
sudo dnf history undo <ID>     # undo a specific transaction

# Clean up
sudo dnf autoremove            # remove no-longer-needed deps
sudo dnf clean all             # purge caches/metadata
```
