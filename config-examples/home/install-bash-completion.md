```bash
# Update and install bash-completion from package manager
sudo apt update
sudo apt install bash-completion

# Edit .bashrc
nano ~/.bashrc

# enable bash completion in interactive shells
if [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
fi
```


