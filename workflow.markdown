# Docs Workflow (Better Git it in Your Soul)

## Abstract

The docs team uses a relatively simple git workflow based on [GitHub Flow](https://guides.github.com/overviews/flow/) (not to be confused with Git Flow). In GitHub Flow, team members create branches off of "master" to work on, then submit a pull request to have their changes deployed. You should definitely read that page if you haven't already; it gives a great high-level overview of the process.

The classic GitHub Flow is great for more involved docs projects, but it's overkill for much of the work that we do. On docs, we relax it in two important ways:

  1. If you're making a fairly small change and you feel like you can get it right in one commit, then go ahead and commit to master.
  2. If you think your branch is ready to merge and you don't see any need for review, then it's perfectly fine to merge it yourself and skip the pull request step.

## General Advice

Git is complicated, and new users pretty much always find it frustrating (if not downright scary) at first. That said, I think that the all-too-common approach of "just teach people the five basic commands and hope for the best" actually does more harm than good. Taking the time early on to learn about the way that git organizes commits and branches will not only make the rest of the process vastly more intuitive, it will save you loads of time and frustration in the future.

A good goal is to be able to draw what's going on in the form of a graph like this:

![Git Graph](graph.png)

There are countless tutorials and books out there, and you may find some more suited to your learning style than others. [Atlassian's Git Tutorial](https://www.atlassian.com/git/tutorial) is a great, highly visual guide to git concepts. For a more comprehensive approach, several of us on the team like O'Reilly's [Version Control with Git](http://www.amazon.com/Version-Control-Git-collaborative-development/dp/1449316387), and recommend it for people who are willing to put in a bit more time.

It's not a tutorial in itself, but one way that you can build up your mental model of git processes is to use a tool like [Explain Git With D3](http://onlywei.github.io/explain-git-with-d3/), which lets you type in git commands and see how they affect the graph immediately.

## Setting Up

### Install git

  1. [Download git](http://git-scm.com/downloads) and run the installer.
  2. Follow GitHub's [instructions for generating an SSH key](https://help.github.com/articles/generating-ssh-keys).
  3. Download the [GitHub for Mac](https://mac.github.com/release-notes.html) application if you prefer a graphical interface. Using the app is explained in more detail in the [quickstart guide](quickstart.markdown).

### Helpful Aliases and Settings

You can save yourself a lot of typing at the command line and build better habits by setting up git **aliases** for common commands---or even sequences of commands. Aliases are defined in `~/.gitconfig` in the `[alias]` section like so:

    [alias]
      ci = commit

Once that's defined, you can type `git ci` instead of `git commit` and save yourself a few keystrokes. Here are a few more along similar lines:

      st = status
      br = branch
      co = checkout

That's fine, but aliases can get much more complicated:

      graph = log --all --graph --decorate --oneline -n30

The above alias sets up a new command, `git graph`, that shows a colorized history of recent commits with a graph.

While you're editing `~/.gitconfig`, you should probably add the following lines at the bottom:

    [pull]
      ff = only
      rebase = true

These settings change some potentially annoying behavior of `git pull` in two important ways:

  1. `git pull` will not merge unless it can fast forward, i.e., unless there are no local changes that haven't been published.
  2. If there are local changes, it will try to [rebase](https://www.atlassian.com/git/tutorial/rewriting-git-history#!rebase) them to keep the history nice and neat.
  3. If you have local changes that conflict with the master branch, you'll have to resolve those [merge conflicts](#merge-conflicts)

Neither of these settings will necessarily prevent merge conflicts, which this document covers in a later section.

### Clone the puppetlabs/puppet-docs repository

You should run `git clone https://github.com/puppetlabs/puppet-docs/ --origin upstream` to make sure that the puppetlabs repository is named `upstream` rather than the ambiguous `origin`.

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

### Committing

We've historically been pretty lax when it comes to commit messages, but there are a few things that you should keep in mind:

  1. Commit messages are not only open to the public, they're proudly displayed in a sidebar on the docs site. Remember that when you're writing them.
  2. Give a clear indication of what the commit relates to up front. The first 50 characters or so of a commit message are the most important, because sometimes that's all you can see when you're looking through the history of a branch.
  3. If the commit resolves a ticket, reference the ticket number somewhere in the commit message.

### Branching

[GitHub Flow](https://guides.github.com/overviews/flow/) mandates that all work be done on a branch other than master, but that's not really practical for us. You should at least *consider* making a new branch for each task, but it's not required for quick changes.

It's a good idea to keep your branch online by pushing it to either your own fork, the puppetlabs/puppet-docs repo, or (if you're working on sensitive material) the puppetlabs/puppet-docs-private repo.

### Merging/Pull Requests

You are welcome to merge your work into `master` yourself if you think it's ready.

  1. Make sure all branches are current: `git up`
  2. Switch to the master branch: `git checkout master`
  3. Merge your branch: `git merge <BRANCH>` (this might trigger a [merge conflict](#merge-conflicts))
  4. Push your updated master branch: `git push`

If you don't want it to go live until somebody else has had a look at it, here's what you should do:

  1. Make sure all branches are current: `git up`
  2. Switch to your branch: `git checkout <BRANCH>`
  3. Rebase your branch against the master branch: `git rebase upstream/master` (this might trigger a [merge conflict](#merge-conflicts))
  4. Upload your branch: `git push <BRANCH>`
  5. [Create a pull request](https://help.github.com/articles/creating-a-pull-request) targeting the `master` branch.
  6. In the body of the pull request, @tag at least one person and let them know what you need (technical review, copy-editing, etc.). Politely mention any time constraints you might be under.

## Less-Than-Ideal Situations

From time to time, you will inevitably find yourself in a shallow pit of git-related despair.

### Merge Conflicts



### Amending Commits
### Basing Work on Content That's Still Being Updated
### Rejected Commits
