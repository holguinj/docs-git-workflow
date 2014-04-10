# Docs Workflow (STUNNED WITH ANXIETY)

## Abstract

The docs team uses a relatively simple git workflow based on [GitHub Flow](https://guides.github.com/overviews/flow/) (not to be confused with Git Flow). In GitHub Flow, team members create branches off of "master" to work on, then submit a pull request to have their changes deployed. You should definitely read that page if you haven't already; it gives a great high-level overview of the process.

The classic GitHub Flow is great for more involved docs projects, but it's overkill for much (if not most) of the work that we do. On docs, we relax it in two important ways:

1. If you're making a fairly small change and you feel like you can get it right in one commit, then go ahead and commit to master.
2. If you think your branch is ready to merge and you don't see any need for review, then it's perfectly fine to merge it yourself and skip the pull request step.

## Setting Up
### Install git

1. [Download git](http://git-scm.com/downloads) and run the installer. 
2. Follow GitHub's [instructions for generating an SSH key](https://help.github.com/articles/generating-ssh-keys).

### Clone the puppetlabs/puppet-docs repository

You should run `git clone https://github.com/puppetlabs/puppet-docs/ --origin upstream` to make sure that the puppetlabs repository is named `upstream` rather than the ambiguous `origin`.

### Add your own remote (optional)

It's not required, but you should consider forking the puppet-docs repo and adding a remote for it. Just click the "Fork" button at the top of the [GitHub page for the repo](https://github.com/puppetlabs/puppet-docs) and then run the following command:

    git remote add myname https://github.com/myname/puppet-docs
    
Once you do that, you can push your commits to `myname` instead of `upstream` and they won't be deployed to the site.

## Writing and Publishing



### Branching
### Committing
### Merging
### Publishing

## Less-Than-Ideal Situations
### Merge Conflicts
### Amending Commits
### Basing Work on Content That's Still Being Maintained
### Rejected Commits
