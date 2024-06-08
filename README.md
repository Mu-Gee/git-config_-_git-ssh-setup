# First-Time Git Setup

This repo should help you setup Git for the first time after install and also guide you on how to setup SSH for Git  to Github

***Note: This guide assumes you have already/just installed Git on your system***

Now that you have Git on your system, you’ll want to do a few things to customize your Git environment. You should have to do these things only once on any given computer; they’ll stick around between upgrades. You can also change them at any time by running through the commands again.

Git comes with a tool called `git config` that lets you get and set configuration variables that control all aspects of how Git looks and operates. Indepth explanation of where these variables are stored can be found [here](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup "git  configuration variables").

You can view all of your settings and where they are coming from using:

```
$ git config --list --show-origin
```

Now, let's get started.


## Your Identity

The first thing you should do when you install Git is to set your user name and email address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you start creating:

```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

Again, you need to do this only once if you pass the `--global` option, because then Git will always use that information for anything you do on that system. If you want to override this with a different name or email address for specific projects, you can run the command without the `--global` option when you’re in that project.

***Note: The email used here will be visisble on all your commits both private and public, it is therefore adviced to use the email Github provides you for making changes to a repository. It should look something like this*** `12345678+your_github_username@users.noreply.github.com`

## Your default branch name

By default Git will create a branch called master when you create a new repository with `git init`. From Git version 2.28 onwards, you can set a different name for the initial branch.

To set main as the default branch name do:

```
git config --global init.defaultBranch main
```

## Checking Your Settings

If you want to check your configuration settings, you can use the `git config --list` command to list all the settings Git can find at that point:

```
git config --list
```

You should get an output similar to this:

```
user.name=John Doe
user.email=johndoe@example.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```

Now that you have Git configured it's time to start using it. Now let's configure SSH for Git to Github so that you can easily work with your remote reposistories from the CLI

## Generating a new SSH key and adding it to the ssh-agent

You can access and write data in repositories on GitHub.com using SSH (Secure Shell Protocol). When you connect via SSH, you authenticate using a private key file on your local machine. For more information, see ["About SSH."](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh "Using the SSH protocol, you can connect and authenticate to remote servers and services. With SSH keys, you can connect to GitHub without supplying your username and personal access token at each visit. You can also use an SSH key to sign commits.")

If you don't already have an SSH key, you must generate a new SSH key to use for authentication. If you're unsure whether you already have an SSH key, you can check for existing keys. For more information, see  ["Checking for existing SSH keys."](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh "Before you generate an SSH key, you can check to see if you have any existing SSH keys.")

### Generating a new SSH key
The instructions below cover generating a new ssh key in Linux for Windows see [Windows](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=windows "Generating ssh keys for Windows") and for Mac see [Mac](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=mac "Generating ssh keys for Mac")

1. Open Terminal
2. Paste the text below, replacing the email used in the example with your GitHub email address.

```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
***Note: If you are using a legacy system that doesn't support the Ed25519 algorithm, use:***
```
 ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
This creates a new SSH key, using the provided email as a label.

When you're prompted to "Enter a file in which to save the key", you can press Enter to accept the default file location. Please note that if you created SSH keys previously, ssh-keygen may ask you to rewrite another key, in which case we recommend creating a custom-named SSH key. To do so, type the default file location and replace id_ALGORITHM with your custom key name.

`> Enter a file in which to save the key (/home/YOU/.ssh/id_ALGORITHM):[Press enter]`

3. At the prompt, type a secure passphrase. For more information, see ["Working with SSH key passphrases."](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases "You can secure your SSH keys and configure an authentication agent so that you won't have to reenter your passphrase every time you use your SSH keys.")

`> Enter a file in which to save the key (/home/YOU/.ssh/id_ALGORITHM):[Press enter]`

### Adding your SSH key to the ssh-agent

Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key.

1. Start the ssh-agent in the background.

```
eval "$(ssh-agent -s)"
```
`> Agent pid 59566`

Depending on your environment, you may need to use a different command. For example, you may need to use root access by running `sudo -s -H` before starting the ssh-agent, or you may need to use `exec ssh-agent bash` or `exec ssh-agent zsh` to run the ssh-agent.

2. Add your SSH private key to the ssh-agent.

If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_ed25519 in the command with the name of your private key file.
```
ssh-add ~/.ssh/id_ed25519
```

3. Add the SSH public key to your account on GitHub.

### Adding a new SSH key to your GitHub account

To configure your account on GitHub.com to use your new (or existing) SSH key, you'll also need to add the key to your account.

1. Copy the SSH public key to your clipboard.

If your SSH public key file has a different name than the example code, modify the filename to match your current setup. When copying your key, don't add any newlines or whitespace.

```
$ cat ~/.ssh/id_ed25519.pub
# Then select and copy the contents of the id_ed25519.pub file
# displayed in the terminal to your clipboard
```

***Tip: Alternatively, you can locate the hidden .ssh folder, open the file in your favorite text editor, and copy it to your clipboard.***

2. In the upper-right corner of any page on GitHub, click your profile photo, then click Settings.

3. In the "Access" section of the sidebar, click SSH and GPG keys.

4. Click New SSH key or Add SSH key.

5. In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal laptop, you might call this key "Personal laptop".

6. Select the type of key, either authentication or signing.

7. In the "Key" field, paste your public key.

8. Click Add SSH key.

9. If prompted, confirm access to your account on GitHub.

### Testing your SSH connection

After you've set up your SSH key and added it to GitHub, you can test your connection.

1. Open Terminal.

2. Enter the following:
```
ssh -T git@github.com
```
You may see a warning like this:

> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
> ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
> Are you sure you want to continue connecting (yes/no)?

3. Verify that the fingerprint in the message you see matches GitHub's public key fingerprint. If it does, then type yes:

> Hi USERNAME! You've successfully authenticated, but GitHub does not
> provide shell access.

You may see this error message:

>...
Agent admitted failure to sign using the key.
debug1: No more authentication methods to try.
Permission denied (publickey).