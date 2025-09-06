# `chmod` Quick Reference

Common `chmod` permissions with meanings and typical use.

| Octal | Meaning (Owner / Group / Others) | Common Use     |
| ----- | -------------------------------- | -------------- |
| `600` | rw- / --- / ---                  | Private file (only owner can read/write, e.g. `authorized_keys`)         |
| `644` | rw- / r-- / r--                  | Public-readable files (e.g. web files, configs)                          |
| `700` | rwx / --- / ---                  | Private directory (only owner can enter/traverse)                             |
| `755` | rwx / r-x / r-x                  | Public directories/executables (everyone can traverse, owner can modify) |
| `777` | rwx / rwx / rwx                  | Full access for all (**RARELY SAFE** avoid unless temporary test)        |
