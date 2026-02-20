# Linux User and Group Management Commands

<details>
<summary><b>adduser</b></summary>

To add a user:
```bash
adduser doe

To add a user doe with a different shell zsh:
sudo adduser doe --shell /bin/zsh

To add a user doe with different home directory thirstyminds:
sudo adduser doe --home /home/thirstyminds/

To Add a existing user doe to a Specific Group devops
sudo adduser doe devops
</details>

<details>
<summary><b>addgroup</b></summary>

To add a new group devops

Bash

sudo addgroup devops
To Create a System Group

Bash

sudo addgroup --system nginx
To View Group Information

Bash

grep devops /etc/group
</details>

<details>
<summary><b>deluser</b></summary>

To delete an user account doe and Keep Home Directory

Bash

sudo deluser doe
To delete a user doe and their home directory

Bash

sudo deluser --remove-home doe
To remove a user doe from a specific group devops

Bash

sudo deluser doe devops
To delete user account doe and backup the doe’s home directory into /backup_dir

Bash

sudo deluser --backup-to /backup_dir doe
</details>

<details>
<summary><b>delgroup</b></summary>

To remove a group devops from the system

Bash

sudo delgroup devops
To Delete a System Group

Bash

sudo delgroup --system nginx
sudo delgroup --system apache
To Simulate Group Deletion of devops

Bash

sudo delgroup --dry-run devops
</details>

<details>
<summary><b>useradd</b></summary>

To add a new user doe

Bash

sudo useradd doe
To Create a user doe with a home directory /home/doe

Bash

sudo useradd -m doe
To create a User doe with a Specific User ID 1007

Bash

sudo useradd -u 1007 doe
To Create a User doe with Account Expiry Date

Bash

sudo useradd -e 2025-12-31 doe
To check

Bash

chage -l doe
</details>

<details>
<summary><b>userdel</b></summary>

To delete a user account doe

Bash

sudo userdel doe
To remove the user’s and home directory and mail spool of user doe

Bash

sudo userdel -r doe
</details>

<details>
<summary><b>usermod</b></summary>

To add supplementary and primary group to user

Bash

sudo usermod -aG sudo doe
To set user account expiry date

Bash

sudo usermod -e 2025-12-31 doe
To lock user account

Bash

sudo usermod -L doe
To unlock user account

Bash

sudo usermod -U doe
</details>

<details>
<summary><b>groupadd</b></summary>

To create a group devops

Bash

sudo groupadd devops
To create a group devops with specific groupid

Bash

sudo groupadd devops -g 1234
To Verify Group Creation

Bash

grep devops /etc/group
</details>

<details>
<summary><b>groupdel</b></summary>

To delete a group

Bash

sudo groupdel developers
To verify group deletion

Bash

getent group developers
</details>

<details>
<summary><b>groupmod</b></summary>

To change the group “devops” to “developers”

Bash

sudo groupmod -n developers devops
To change groupid of a group devops to 1234

Bash

sudo groupmod -g 1234 devops
</details>

<details>
<summary><b>groupmems</b></summary>

To list all members of a group developers

Bash

sudo groupmems -g developers -l
To make the user doe a member of the group devops

Bash

sudo groupmems -g devops -a doe
To delete/remove a user doc from a group devops

Bash

sudo groupmems -g devops -d doe
</details>

<details>
<summary><b>gpasswd</b></summary>

To set a group password

Bash

sudo gpasswd developers
To give user alice administrative rights to the group developers

Bash

sudo gpasswd -A alice developers
To lock a group developers

Bash

sudo gpasswd -r developers
</details>

<details>
<summary><b>passwd</b></summary>

To change password for root

Bash

sudo passwd root
To display user status Information of doe

Bash

sudo passwd -S doe
To display information of all users

Bash

sudo passwd -Sa
To delete user’s password

Bash

sudo passwd -d doe
</details>

<details>
<summary><b>chage</b></summary>

To view the account aging information of user doe

Bash

chage -l doe
To set the last password change date to your specified date for user doe

Bash

chage -d 2025-12-31 doe
To set the date when the account should expire

Bash

chage -E 2025-12-31 doe
To remove expiration

Bash

sudo chage -E -1 doe
To specify the maximum number of days between password change

Bash

chage -M 90 doe
</details>

<details>
<summary><b>chpasswd</b></summary>

update passwords in batch mode

Bash

sudo chpasswd
storing username and password in a file and give input to chpasswd

Bash

cat > password.txt
sudo chpasswd < password.txt
To apply encryption algorithm on password

Bash

sudo chpasswd -c SHA512
sudo chpasswd -c SHA256
sudo chpasswd --md5
</details>

<details>
<summary><b>finger</b></summary>

To display information about system user and user doe

Bash

finger doe
To get idle status and login details of a user

Bash

finger -s doe
To show multiple users at once

Bash

finger doe alice john
</details>

<details>
<summary><b>id</b></summary>

To print your own id without any options

Bash

id
To find a specific user doe id

Bash

id -u doe
To find out UID and all groups associated with a username

Bash

id doe
To find out all the groups a user doe belongs

Bash

id -nG doe
</details>

<details>
<summary><b>who / whoami / logname</b></summary>

To print who command output without options

Bash

who
To print the login names and total number of logged on users

Bash

who -q
To view the time of last system boot

Bash

who -b
To check the current runlevel

Bash

who -r
To show the name of the currently logged-in user

Bash

whoami
To display user’s login name

Bash

logname
</details>

<details>
<summary><b>last / w / users</b></summary>

To list of the most recent logins and logouts of users

Bash

last
To list last five users logged in

Bash

last -5
To display the login and logout time including the dates

Bash

last -F
To display within a specific time period.(-s) since and (-t) until

Bash

last -s yesterday -t today
To Show who is logged on and what they are doing

Bash

w
To print the user names of users currently logged in

Bash

users
To Combine with wc to count logged-in users

Bash

users | wc -w
</details>

<details>
<summary><b>chgrp</b></summary>

To Change group ownership of a file

Bash

sudo chgrp devops project.txt
To change a directory example_dir group ownership

Bash

sudo chgrp devops example_dir
To recursively change group ownership

Bash

sudo chgrp -R devops example_dir
</details>

<details>
<summary><b>login / logout / loginctl / nologin</b></summary>

To log in to the system as user doe (preserves env variables)

Bash

login -p doe
To login to a domain

Bash

login test.hashlabs.in
To Use with -f option (automatic login)

Bash

login -f alice
To logout the user from the current session

Bash

logout
To Show all sessions and attributes

Bash

loginctl -a
To display session configuration message

Bash

loginctl show-session
To list currently logged in users

Bash

loginctl list-users
To Prevent a user from logging in

Bash

sudo usermod -s /sbin/nologin ftpuser
create a custom message file shown by nologin

Bash

echo "Access to this system is restricted." | sudo tee /etc/nologin.txt
</details>

<details>
<summary><b>su / sudo / sudoreplay / setsid / faillog</b></summary>

To Switch to the root user

Bash

su
su command to switch users without a password

Bash

su - alice
To Use su with sudo command

Bash

sudo su - alice
To run command as a root user

Bash

sudo apt update
To List user privileges with sudo

Bash

sudo -l
To add users to the sudoers file

Bash

sudo visudo
To List recorded sessions

Bash

sudo sudoreplay -l
To Run myscript.sh in the background independently

Bash

setsid myscript.sh &
To Show all failed login attempts

Bash

sudo faillog
To lock an account doe for 2 minute / 120 seconds after failed login

Bash

sudo faillog -l 60 -u doe
</details>

<details>
<summary><b>chfn / newusers</b></summary>

To Change your own finger information interactively

Bash

chfn
To change the full name on the account from alice to doe

Bash

sudo chfn -f doe alice
create users details in a file and run newusers

Bash

sudo vim users.txt
# Format: alice:$6$abcd1234$xyz:1001:1001:Alice:/home/alice:/bin/bash
sudo chmod 0600 users.txt
sudo newusers users.txt
</details>

<details>
<summary><b>wall / write / mesg / newgrp</b></summary>

To send a message on the terminals of all logged-in users

Bash

sudo wall "The system will be rebooted in 20 minutes."
To pipe the output of another command to wall

Bash

echo "save your work." | wall
To write a message to user2 from user1

Bash

write user2
To pipe a message to write

Bash

echo "Hello from user1" | write user2
To display the current write status of your terminal

Bash

mesg
To disallow/allow write access to your terminal

Bash

mesg n
mesg y
Log into a new group

Bash

newgrp devops
</details>
