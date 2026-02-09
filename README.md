# README

## SSH

### Sign in:

If the user has an authorized key then the below will immediately connect them.
If not, then they will have to enter their own password when prompted.

```sh
# if their local username is the same as remote, or ssh config maps a username:
ssh keyboard.town

# with explicit username:
ssh <username>@keyboard.town
```

### Change your own password

Users can change their own password if they know their current password:

```sh
ssh keyboard.town
passwd <username>
<enter new password>
```

### Forgot password

If the user logs in with a password (not an SSH key), reset it from the VPS as root (or a sudo user):

Ask the Admin to SSH in as root, then set a new password:

```sh
ssh keyboard.town
su
<enter root password>
passwd <username>
<enter new password>
```

If the user is meant to use SSH keys only, don’t set a password—add/replace their public key instead by editing:

```sh
nano /home/username/.ssh/authorized_keys
```
