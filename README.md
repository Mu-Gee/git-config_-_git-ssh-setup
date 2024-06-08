# First-Time Git Setup

This repo should help you setup Git for the first time after install and also guide you on how to setup SSH for Git  to Github

***Note: This guide assumes you have already/just installed Git on your system***

Now that you have Git on your system, you’ll want to do a few things to customize your Git environment. You should have to do these things only once on any given computer; they’ll stick around between upgrades. You can also change them at any time by running through the commands again.

Git comes with a tool called `git config` that lets you get and set configuration variables that control all aspects of how Git looks and operates. Indepth explanation of where these variables are stored can be found [here](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup "git  configuration variables"). Now let's get started.

## Your Identity

The first thing you should do when you install Git is to set your user name and email address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you start creating:

```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

Again, you need to do this only once if you pass the `--global` option, because then Git will always use that information for anything you do on that system. If you want to override this with a different name or email address for specific projects, you can run the command without the `--global` option when you’re in that project.

***Note: The email used here will be visisble on all your commits both private and public, it is therefore advicedto use the email Github provides you for making changes to a repository. It should look something like this*** `12345678+your_github_username@users.noreply.github.com`

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
>user.name=John Doe
user.email=johndoe@example.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```
user.name=John Doe
user.email=johndoe@example.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```


You can view all of your settings and where they are coming from using:

```
$ git config --list --show-origin
```
