# Docs Workflow (STUNNED WITH ANXIETY)

## Abstract

The docs team uses a relatively simple git workflow based on [GitHub Flow](https://guides.github.com/overviews/flow/) (not to be confused with Git Flow). In GitHub Flow, team members create branches off of "master" to work on, then submit a pull request to have their changes deployed. You should definitely read that page if you haven't already; it gives a great high-level overview of the process.

The classic GitHub Flow is great for more involved docs projects, but it's overkill for much (if not most) of the work that we do. On docs, we relax it in two important ways:

  1. If you're making a fairly small change and you feel like you can get it right in one commit, then go ahead and commit to master.
  2. If you think your branch is ready to merge and you don't see any need for review, then it's perfectly fine to merge it yourself and skip the pull request step.

## General Advice

Git is complicated, and new users pretty much always find it frustrating at first, if not downright scary. That said, I think that the all-too-common approach of "just teach people the five basic commands and hope for the best" actually does more harm than good. Taking the time early on to learn about the way that git organizes commits (the impressively-named Directed Acyclic Graph) will not only make the rest of the process vastly more intuitive, it will save you loads of time and frustration in the future.

There are countless tutorials and books out there, and you may find some more suited to your learning style than others. Several of us on the team like O'Reilly's [Version Control with Git](http://www.amazon.com/Version-Control-Git-collaborative-development/dp/1449316387), and recommend it for people who are willing to put in a bit of time.

It's not a tutorial in itself, but one way that you can build up your mental model of git processes is to use a tool like [Explain Git With D3](http://onlywei.github.io/explain-git-with-d3/), which lets you type in git commands and see how they affect the graph immediately.

## Setting Up
### Install git

  1. [Download git](http://git-scm.com/downloads) and run the installer.
  2. Follow GitHub's [instructions for generating an SSH key](https://help.github.com/articles/generating-ssh-keys).
  3. Download the [GitHub for Mac](https://mac.github.com/release-notes.html) application if you prefer a graphical interface.

### Helpful Aliases and Settings

You can save yourself a lot of typing at the command line and build better habits by setting up git **aliases** for common commands---or even sequences of commands. Aliases are defined in `~/.gitconfig` in the `[alias]` section like so:

    [alias]
      ci = commit

Once that's defined, you can type `git ci` instead of `git commit` and save yourself a few keystrokes. That's fine, but aliases can get much more complicated:

      graph = log --all --graph --decorate --oneline -n30

The above alias sets up a new command, `git graph`, that shows a colorized history of recent commits with a graph.

While you're editing `~/.gitconfig`, you should probably add the following lines at the bottom:

    [pull]
      ff = only
      rebase = true

These settings change some potentially annoying behavior of `git pull` in two important ways:

  1. `git pull` will not merge unless it can fast forward, i.e., unless there are no local changes that haven't been published.
  2. If there are local changes, it will try to rebase them to keep the history nice and neat.

Neither of these settings will necessarily prevent merge conflicts, which this document covers in a later section.

### Clone the puppetlabs/puppet-docs repository

You should run `git clone https://github.com/puppetlabs/puppet-docs/ --origin upstream` to make sure that the puppetlabs repository is named `upstream` rather than the ambiguous `origin`.

If you're using the GUI app, you can [click here to clone the repo](github-mac://openRepo/https://github.com/puppetlabs/puppet-docs).

### Add your own remote (optional)

It's not required, but you should consider forking the puppet-docs repo and adding a remote for it. Just click the "Fork" button at the top of the [GitHub page for the repo](https://github.com/puppetlabs/puppet-docs) and then run the following command:

    git remote add myname https://github.com/myname/puppet-docs

Once you do that, you can push your commits to `myname` instead of `upstream` and they won't be deployed to the site.

**Note:** This is one of the areas where the GUI app falls short. If you want to use multiple remotes, you'll have to use the command line (at least to push).

## Writing and Publishing

Let's look at a simple example: fixing a typo in `index.markdown`. Here's how it should go:

  1. `git pull` the repo to make sure that you have the latest version.
  2. Edit `index.markdown` your text editor of choice.
  3. `git status` should show something like this:

      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.markdown

  4. Use `git add index.markdown` to stage the file so that it will be included in the next commit.
  5. Commit the change with `git commit -m "Fixed a typo in the index`.
  6. Publish the commit with `git push`.

It doesn't get much simpler than that, and often that's all you need. The commit message in step 5 above (marked with the `-m` or `--message` flag)

### Branching
### Committing
### Merging
### Publishing

## Less-Than-Ideal Situations
### Merge Conflicts
### Amending Commits
### Basing Work on Content That's Still Being Updated
### Rejected Commits
