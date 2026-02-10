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

## Dokku Apps

### Configuring a Dokku `git` "remote"

Projects are pushed to Dokku by app name. In `git`, each app has its own "remote":

```ini
[remote "<remote-name>"]
	url = dokku@dokku:<app-name>
	fetch = +refs/heads/*:refs/remotes/<remote-name>/*
```

To push the same project to a different remote (eg, the dev version of a project):

1. Create a new Dokku app
2. Duplicate the remove in your project's `.git/config`. Change the remote name on the 1st and 3rd line of the config, and set the new project app on the second line.

```sh
# Push the current HEAD to whichever "remote" you want:
git push <remote-name>
```

### Pushing to Dokku!

In order to push to Dokku, you must have an ssh key configured in Dokku. To do
this, copy the contents of your public key file:

```sh
cat ~/.ssh/id_ed25519.pub
```

Then, in Dokku, add the public key:

```sh
echo "$CONTENTS_OF_YOUR_PUBLIC_SSH_KEY_HERE" | dokku ssh-keys:add KEY_NAME
```
