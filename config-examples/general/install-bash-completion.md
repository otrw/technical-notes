# Install and enable bash completion

1. Install and enable `bash-completion` from your package manager:

```bash
sudo apt update
sudo apt install bash-completion
```

2. Edit your `.bashrc`

```bash
nano ~/.bashrc
```

3. Add the following to enable bash completion.

```bash
if [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
fi
```

**NOTE**: This is enabled by default in most distribution and these steps are not required.
