# Linux User and Group Management Commands

A comprehensive cheat sheet for managing users, groups, passwords, and sessions in Linux. 

> **Note:** Commands like `adduser` and `addgroup` are interactive, high-level Perl scripts (common on Debian/Ubuntu), while `useradd` and `groupadd` are the low-level native binaries. 

---

## 1. User Management

### `adduser` (High-level, Interactive)
* **Add a new user:** `sudo adduser doe`
* **Add user with a specific shell:** `sudo adduser doe --shell /bin/zsh`
* **Add user with a custom home directory:** `sudo adduser doe --home /home/thirstyminds/`
* **Add an existing user to a specific group:** `sudo adduser doe devops`

### `useradd` (Low-level)
* **Add a new user:** `sudo useradd doe`
* **Create user with a home directory:** `sudo useradd -m doe`
* **Create user with a specific User ID (UID):** `sudo useradd -u 1007 doe`
* **Create user with an account expiry date:** `sudo useradd -e 2025-12-31 doe`

### `usermod` (Modify User)
* **Add user to a supplementary group (append):** `sudo usermod -aG sudo doe`
* **Set account expiry date:** `sudo usermod -e 2025-12-31 doe`
* **Lock user account:** `sudo usermod -L doe`
* **Unlock user account:** `sudo usermod -U doe`
* **Change user's login shell (to prevent login):** `sudo usermod -s /sbin/nologin ftpuser`

### `deluser` & `userdel` (Delete User)
* **Delete user (keep home directory):** `sudo deluser doe`
* **Delete user and their home directory:** `sudo deluser --remove-home doe`
* **Remove user from a specific group:** `sudo deluser doe devops`
* **Delete user and backup home directory:** `sudo deluser --backup-to /backup_dir doe`
* **Delete user account (low-level):** `sudo userdel doe`
* **Delete user, home directory, and mail spool:** `sudo userdel -r doe`

### `newusers` (Batch Create Users)
* **Create multiple users from a file:** ```bash
  sudo vim users.txt
  # Format: username:password:UID:GID:User Info:Home Dir:Command Shell
  # alice:$6$abcd1234$xyz:1001:1001:Alice:/home/alice:/bin/bash
  sudo chmod 0600 users.txt
  sudo newusers users.txt
chfn (Change Finger Info)
Change user details interactively: chfn

Change full name: sudo chfn -f "John Doe" alice

Change work phone number: sudo chfn -w 9999988888 doe

2. Group Management
addgroup & groupadd (Create Groups)
Add a new group: sudo addgroup devops  OR  sudo groupadd devops

Create a system group: sudo addgroup --system nginx

Create group with a specific Group ID (GID): sudo groupadd devops -g 1234

groupmod (Modify Groups)
Rename a group: sudo groupmod -n developers devops

Change Group ID (GID): sudo groupmod -g 1234 devops

delgroup & groupdel (Delete Groups)
Delete a group: sudo delgroup devops  OR  sudo groupdel developers

Delete a system group: sudo delgroup --system apache

Simulate group deletion (Dry run): sudo delgroup --dry-run devops

groupmems & chgrp (Manage Members & Ownership)
List all members of a group: sudo groupmems -g developers -l

Add user to a group: sudo groupmems -g devops -a doe

Remove user from a group: sudo groupmems -g devops -d doe

Change group ownership of a file: sudo chgrp devops project.txt

Change group ownership of a directory recursively: sudo chgrp -R devops example_dir

newgrp (Switch Groups)
Log into a new group (changes effective GID for the session): newgrp devops

3. Passwords and Aging
passwd & chpasswd
Change root password: sudo passwd root

Display user password status: sudo passwd -S doe

Display password status for all users: sudo passwd -Sa

Delete user’s password (make passwordless): sudo passwd -d doe

Update passwords in batch mode: ```bash
cat > password.txt

user:password
sudo chpasswd < password.txt

Apply specific encryption (SHA512): sudo chpasswd -c SHA512

gpasswd (Group Passwords)
Set a group password: sudo gpasswd developers

Give a user administrative rights over a group: sudo gpasswd -A alice developers

Lock a group: sudo gpasswd -r developers

chage (Password Aging & Expiry)
View account aging info: chage -l doe

Set exact date for account expiry: sudo chage -E 2025-12-31 doe

Remove expiration: sudo chage -E -1 doe

Set max days between password changes: sudo chage -M 90 doe

4. Viewing User Information
id: Print user and group IDs (id doe, id -nG doe).

who: Show who is logged on (who -q for count, who -b for last boot).

whoami: Show the currently logged-in username.

w: Show who is logged on and what they are doing.

users: Print names of currently logged-in users.

finger: Display detailed info about a user (finger doe).

logname: Display initial login name.

last: List recent logins/logouts from /var/log/wtmp (last -5, last -s yesterday -t today).

5. Sessions and Privileges
Privileged Access
Switch to root user: su -

Switch user without environment: su alice

Run a command as root: sudo <command>

Edit the sudoers file: sudo visudo

List sudo privileges for current user: sudo -l

Replay recorded sudo sessions: sudo sudoreplay -l

Logins & Sessions
Login to the system/domain: login -p doe

Logout of current session: logout

List active sessions: loginctl list-users or loginctl -a

Detach a process from the terminal: setsid myscript.sh &

Login Restrictions
Check failed login attempts: sudo faillog -u doe

Lock account after failed attempts: sudo faillog -l 60 -u doe

Set custom nologin message: echo "Access restricted." | sudo tee /etc/nologin.txt

6. Terminal Communication
wall: Send a message to all logged-in users (sudo wall "System rebooting in 20 mins").

write: Send a message to a specific user (echo "Hello" | write user2).

mesg: Control write access to your terminal (mesg y to allow, mesg n to block).
