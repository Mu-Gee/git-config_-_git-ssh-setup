# First-Time Git Setup

This repo should help you setup Git for the first time after install and also guide you on how to setup SSH for Git  to Github

#### Note: This guide assumes you have already/just installed Git on your system

Now that you have Git on your system, you’ll want to do a few things to customize your Git environment. You should have to do these things only once on any given computer; they’ll stick around between upgrades. You can also change them at any time by running through the commands again.

Git comes with a tool called `git config` that lets you get and set configuration variables that control all aspects of how Git looks and operates. Indepth explanation of where these variables are stored can be found [here](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup "git  configuration variables"). Now let's get started.

### Your Identity

The first thing you should do when you install Git is to set your user name and email address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you start creating:
```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

You can view all of your settings and where they are coming from using:
```$ git config --list --show-origin```