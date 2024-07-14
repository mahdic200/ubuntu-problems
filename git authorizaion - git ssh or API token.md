# introduction to Linux Localdata storage system

in linux for git authorization we have some solution . consider all your personal data will be stored in ~/USER with hidden folders (folders which start with `.` ) . for example all your vscode data , git data , snap data , ssh etc ... . will be stored in this format .

the rest of this page is in the reference [this article tutorial](https://mgimond.github.io/Colby-summer-git-workshop-2021/authenticating-with-github.html#:~:text=Saving%20tokens%20in%20Linux,-To%20temporarily%20cache&text=The%20next%20time%20you%20are%20prompted%20for%20your%20GitHub%20user,this%20file%20is%20not%20encrypted.)

# Personal Access Token (PAT) based authentication

I won't explain how to make Personal Access Token or PAT . I'll explain how to store it in your local Linux desktop machine (instructions are in reference don't worry just read the reference ) .

to temporarily cache the token in Linux use the following command :

```shell
git config --global credential.helper cache
```

Note, however, that the token is only cached for 15 minutes by default. If you want the token to be cached for a longer period of time, add the `'cache --timeout=XX\'` option where XX is time in seconds. For example, to cache the token for 24 hours (86,400 seconds), type:

```shell
git config --global credential.helper cache --timeout=86400
```

to **permanently** cache the token on Linux, type:

```shell
git config credential.helper store
```

The next time you are prompted for your GitHub user name and token, the information will be stored permanently in a `.git-credentials` file under your `home` folder. Note, however, that this file is **not encrypted**. For a more secure permanent solution, you might want to check the _SSH based authentication_ option.

# SSH based authentication

> [!WARNING] can't use usual remote anymore !
> NOTE: if you adopt as SSH based approach to authentication , you will need to connect to your repo via `SSH` . For example , if user `someguy`'s repo name is `someproject` , you would connect to it via :
> 

```shell
git@github.com:someguy/someporject.git
```

> [!WARNING]
> this differs from the HTTPS option adopted in this workshop:

```shell
https://github.com/someguy/someproject.git
```


## checking for existing SSH keys

you might or might not already have public keys under `~/.ssh` file .

```shell
ls -al ~/.ssh
```

If you do, look for the files ending with `.pub`. The contents of these public keys are used to link your local repos to your GitHub account. By default, the filenames of the public keys are one of the following: `id_ed25519.pub` or `id_rsa.pub`. If these files exist in your `~/.ssh` folder, you can jump to the Adding SSH key to your GitHub account section of this tutorial.

## Generating a new SSH key

follow these instructions
```shell
ssh-keygen -t <DESIRED_ID> -C "<your_github_email_address>"
```

example :

```shell
ssh-keygen -t ed22519 -C "someguy@gmail.com"
```

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/jdcolby/.ssh/id_ed25519):
```

This creates a new SSH key, using the provided email as a label. Accept the default file location and press the `Enter` key.

At the prompt, type a secure passphrase. This passphrase will be used instead of your password when performing a Git/GitHub transaction from your computer, so don’t forget it!

```
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

You will then see an output similar to this:

```
Your identification has been saved in /home/jdcolby/.ssh/id_ed25519
Your public key has been saved in /home/jdcolby/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:AuErG+8I8YUkRbNn1iNiGB/T3P6p4oWtmHA821i3bPO jdcolby@my_college.edu
The key's randomart image is:
+--[ED25519 256]--+
|    ..o.o        |
|.o . o o o       |
|o O o . o .    . |
|.* * o . .  . o  |
|*++ + . S  . E   |
|**oo   .    . .  |
|*++.    .    o   |
|o=o.     . .o.   |
|+o.       ..o..  |
+----[SHA256]-----+
```

## Adding SSH key to the ssh-agent process

Next, you need to add the previously generated key to a process called `ssh-agent`.

```shell
eval "$(ssh-agent -s)"
```

```shell
ssh-add ~/.ssh/id_<the_id_picked>
```

exampl , without any postfix like `.pub`:

```shell
ssh-add ~/.ssh/id_e25519
```



You’ll then be prompted to enter the passphrase used in the earlier step.

```
Enter passphrase for /home/jdcolby/.ssh/id_ed25519:
Identity added: /home/jdcolby/.ssh/id_ed25519 (someguy@gmail.com)
```


### Adding SSH key to your GitHub account

In `~\.ssh` you should see a file ending with `.pub` such as `id_ed25519.pub`. This is the **public** key generated earlier in this tutorial that you will share with your GitHub account.

Open the contents of the `~/.ssh/id_ed25519.pub` file in your home folder.

```shell
cat ~/.ssh/id_ed25519.pub
```

Copy all its contents. It should start with `ssh-ed5519 ...` and end with your email address.

- On **GitHub**, click on your avatar, then select **Settings**.
- On the left sidebar, click on **SSH and GPG keys**.
- Click on **New SSH** **key**.
- Assign a _Title_ for this key (this is only used for your reference but is should be descriptive enough for you to know which client computer it is referencing).
- Paste the key from the `.ssh/id_ed25519.pub` file in the _Key_ field (be careful not to add empty spaces).
- Click **Add SSH** key. You might be prompted to type your GitHub password.

Next, you can test your connection from your Bash environment.

In Bash, type the following (_do not_ substitute the `git@github.com` address).

```shell
ssh -T git@github.com
```

You might see the following warning (including the public key as shown below):

```
The authenticity of host 'github.com (140.82.114.3)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type `yes` to continue.

The next warning should list your account name (e.g. `jdcolby` in this working example).

```
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
Hi jdcolby! You've successfully authenticated, but GitHub does not provide shell access.
```

## Cloning a GitHub repo using SSH

At this point, you should be all set. As mentioned at the beginning of this page, when using SSH to connect to your GitHub repo, you need to use the SSH protocol. For example, to clone `repo1`, you would type:

```shell
git clone git@github.com:someguy/someproject.git
```

You might be prompted for the passphrase that was used in an earlier step when you created the SSH key.

## Converting an existing HTTPS local repo to SSH

If you’ve already cloned a repo using HTTPS on your local computer, you will need to make a few changes to your local repo before benefitting from the SSH system.

First, check that you are indeed using HTTPS:

```shell
git remote -v
```

```
origin  https://github.com/jdcolby/repo1.git (fetch)
origin  https://github.com/jdcolby/repo1.git (push)
```

To change from a HTTPS URL to a SSH URL, type:

```shell
git remote set-url origin git@github.com:jdcolby/repo1.git
```












