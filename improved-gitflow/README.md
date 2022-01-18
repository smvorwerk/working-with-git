# Improved git-flow repository management

A collection of Git extensions to provide high-level repository operations
for Vincent Driessen's [branching model](http://nvie.com/git-model "original
blog post"). This fork adds functionality not added to the original branch.


## Getting started

For the best introduction to get started with `git flow`, please read Jeff
Kreeftmeijer's blog post:

[http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/](http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/)

Or have a look at one of these screen casts:

* [How to use a scalable Git branching model called git-flow](http://buildamodule.com/video/change-management-and-version-control-deploying-releases-features-and-fixes-with-git-how-to-use-a-scalable-git-branching-model-called-gitflow) (by Build a Module)
* [A short introduction to git-flow](http://vimeo.com/16018419) (by Mark Derricutt)
* [On the path with git-flow](https://vimeo.com/codesherpas/on-the-path-gitflow) (by Dave Bock)

A quick cheatsheet was made by Daniel Kummer:

[http://danielkummer.github.io/git-flow-cheatsheet/](http://danielkummer.github.io/git-flow-cheatsheet/)

## Installing git-flow

### Installing on Linux, Unix, etc.

#### Ubuntu

* **Ubuntu 18.04+**: the improved git-flow shell interface is packaged with Ubuntu. You can install the improved git-flow shell interface using:
    ```
    $ sudo apt-get install git-flow
    ```

---
#### Manual Linux Installation
Under *nix, the easiest way to install git-flow is using Rick Osborne's
excellent git-flow installer, which can be run using the following command:

Execute the following shell script:

```shell
	$ wget -q  https://raw.githubusercontent.com/svorwerk-dentsu/working-with-git/raw/develop/improved-gitflow/contrib/gitflow-installer.sh && sudo bash gitflow-installer.sh install stable; rm gitflow-installer.sh
```

### Installing on Mac OS X

#### Install Latest Release with Homebrew
    brew install git-flow-avh

#### Alternatively Install with wget

Even using wget its a one line effort.

```shell
    wget --no-check-certificate -q -O - https://github.com/svorwerk-dentsu/working-with-git/raw/develop/improved-gitflow/contrib/gitflow-installer.sh install stable| sudo bash
```

#### Alternative-Alternative Installation option using curl

```shell
    curl https://raw.githubusercontent.com/svorwerk-dentsu/working-with-git/develop/improved-gitflow/contrib/gitflow-installer.sh > gitflow-installer.sh
    chmod a+x gitflow-installer.sh
```

#### Stable release
    curl -sL https://github.com/svorwerk-dentsu/working-with-git/raw/develop/improved-gitflow/contrib/gitflow-installer.sh | sudo bash -s install stable
    
#### Post installation setup

Install GNU getopt via Homebrew:    

```shell
    brew install gnu-getopt
```

Create a `~/.gitflow_export` with the content `export FLAGS_GETOPT_CMD="$(brew --prefix gnu-getopt)/bin/getopt"`.

If you have installed GNU getopt through other means than Homebrew, substitute `$(brew --prefix gnu-getopt)/bin/getopt` with the location of the GNU getopt file.


## Integration with your shell

For those who use the [Bash](http://www.gnu.org/software/bash/) or [ZSH](http://www.zsh.org)
shell, you can use my [fork of git-flow-completion](https://github.com/svorwerk-dentsu/working-with-git/tree/develop/fork-of-git-flow-completion)
which includes several additions for git-flow (AVH Edition), or you can use the
original [git-flow-completion](http://github.com/bobthecow/git-flow-completion)
project by [bobthecow](http://github.com/bobthecow). Both offer tab-completion
for git-flow subcommands and branch names with my fork including tab-completion
for the commands not found in the original git-flow.



## Versioning

* Version Numbering Scheme.  
Starting with version 1.0.0, the project uses the following scheme:
\<MAJOR\>.\<MINOR\>.\<REVISION\>\



## How to use

Fork the repository.  Then, run:

```shell
git clone -b master git@github.com:<user_or_group_name>/<repository_name>.git
cd <repo_directory>
```

After that initialize the local gitflow repository with `git flow` itself:

```shell
git flow init -d
git flow feature start <your feature>
```

Then, do work and commit your changes.

```shell
git flow feature publish <your feature>
```

When done, open a pull request to your feature branch.


## git flow usage

### Initialization

To initialize a new repo with the basic branch structure, use:

    git flow init [-d]

This will then interactively prompt you with some questions on which branches
you would like to use as development and production branches, and how you
would like your prefixes be named. You may simply press Return on any of
those questions to accept the (sane) default suggestions.

The ``-d`` flag will accept all defaults.

![Screencast git flow init](http://i.imgur.com/lFQbY5V.gif)

### Creating feature/release/hotfix/support branches

* To list/start/finish/delete feature branches, use:

```shell
git flow feature
git flow feature start <name> [<base>]
git flow feature finish <name>
git flow feature delete <name>
```

  For feature branches, the `<base>` arg must be a branch, when omitted it defaults to the develop branch.

* To push/pull a feature branch to the remote repository, use:

```shell
git flow feature publish <name>
git flow feature track <name>
```

* To list/start/finish/delete release branches, use:

```shell
git flow release
git flow release start <release> [<base>]
git flow release finish <release>
git flow release delete <release>
```

  For release branches, the `<base>` arg must be a branch, when omitted it defaults to the develop branch.

* To list/start/finish/delete hotfix branches, use:

```shell
git flow hotfix
git flow hotfix start <release> [<base>]
git flow hotfix finish <release>
git flow hotfix delete <release>
```

  For hotfix branches, the `<base>` arg must be a branch, when omitted it defaults to the production branch.

* To list/start support branches, use:

```shell
git flow support
git flow support start <release> <base>
```

  For support branches, the `<base>` arg must be a branch, when omitted it defaults to the production branch.

### Share features with others

You can easily publish a feature you are working on. The reason can be to allow other programmers to work on it or to access it from another machine. The publish/track feature of gitflow simplify the creation of a remote branch and its tracking.

When you want to publish a feature just use:
```shell
git flow feature publish <name>
```

or, if you already are into the `feature/<name>` branch, just issue:
```shell
git flow feature publish
```

Now if you execute `git branch -avv` you will see that your branch `feature/<name>` tracks `[origin/feature/<name>]`. To track the same remote branch in another clone of the same repository use:
```shell
git flow feature track <name>
```

This will create a local feature `feature/<name>` that tracks the same remote branch as the original one, that is `origin/feature/<name>`.

When one developer (depending on your work flow) finishes working on the feature he or she can issue `git flow feature finish <name>` and this will automatically delete the remote branch. All other developers shall then run:
```shell
    git flow feature delete <name>
```

to get rid of the local feature that tracks a remote branch that no more exist.

### Share hotfixes with others

You can publish an hotfix you are working on. The reason can be to allow other programmers to work on it or validate it or to access it from another machine.

When you want to publish an hotfix just use (as you did for features):
```shell
git flow hotfix publish <name>
```

or, if you already are into the `hotfix/<name>` branch, just issue:
```shell
git flow hotfix publish
```

Other developers can now update their repositories and checkout the hotfix:
```shell
git pull
git checkout hotfix/<name>
```
and eventually finish it:
```shell
git flow hotfix finish
```


### Using Hooks and Filters

For a wide variety of commands hooks or filters can be called before and after
the command.  
The files should be placed in .git/hooks  
In the directory hooks you can find examples of all the hooks available.

