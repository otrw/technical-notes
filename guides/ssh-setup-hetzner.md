# Hetzner: SSH setup

> For creating a disposable playground, use the `root` account for testing and finding your way around.  

> Best practice: create a new user, especially if hosting applications or leaving the VM up 24/7.

1. Create your VM in the Hetzner console and upload your SSH key for `root`.
    
    - Make a note of the IP Address

2. Connect as root and immediately create a normal user (e.g. `user1`):

   ```bash
   # Connect to VM
   ssh root@<your-vm-ip>

   # Create a new user called 'user1'
   adduser user1 

   # Add user to sudo group
   usermod -aG sudo user1

   # Create .ssh directory
   mkdir -p /home/user1/.ssh

   # Copy the ssh key used for root to user1
   cp /root/.ssh/authorized_keys /home/user1/.ssh/

   # Change ownership of .ssh directory to user1
   chown -R user1:user1 /home/user1/.ssh
   
   # .ssh directory: 700 = owner can read/write/enter (rwx), nobody else (only the user can access)
   chmod 700 /home/user1/.ssh
   
   # authorized_keys file: 600 = owner can read/write (rw-), nobody else (only the user can access)
   chmod 600 /home/user1/.ssh/authorized_keys
   ```

> This gives the new user the same key-based login as used with root previously.
   
3. Update SSH config (`/etc/ssh/sshd_config`) to disable direct root login:

   ```
   # Open with nano or vim
   nano /etc/ssh/sshd_config

   # Modify or Add the following lines
   PermitRootLogin no
   PasswordAuthentication no
   ```

4. Restart SSH

   ```bash
   # Depending on the distro, this will be ssh or sshd
   systemctl restart ssh
   ```

5. Test

   ```bash
   # Log in using ssh
   ssh user1@<your-vm-ip>

   # Check username
   whoami

   # Check group membership
   groups
   ```
