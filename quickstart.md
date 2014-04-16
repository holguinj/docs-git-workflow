# GitHub App Quickstart

This document gives a quick tour of the [GitHub app](https://mac.github.com/release-notes.html) with the goal of quickly orienting people to the docs team's workflow. Even if you've never used git before, this guide should help you begin to make and publish changes to the site.

That said, this is not a replacement for [workflow guide](workflow.markdown), which provides a much more comprehensive look at the process. The GUI app may be fast and convenient, but it hides most of what's really going on and using it is counter-productive if you want to really learn git.

## Setup

Sign up for a [GitHub](https://www.github.com) account if you don't have one already, then download the [GitHub app](https://mac.github.com/release-notes.html) and install it.

Once you're logged in with the app, you can [click here to clone the puppetlabs/puppet-docs repo](github-mac://openRepo/https://github.com/puppetlabs/puppet-docs). Cloning it doesn't require any special permissions, but you'll need to talk to Ops and have them add you to our organization before you can publish your changes.

## Making one-off changes

To illustrate the process of making small changes to the site, let's look at the example of correcting a typo. I've deleted a couple of extra spaces in `source/index.markdown` and saved the file, so now the GitHub app is showing this:

![Commit Dialog](commit_dialog.jpg)

  1. This section shows the target branch for the commit. The `master` branch is the one from which the site is actually generated, so that's where we want to be right now.
  2. This is the "Commit & Sync" toggle. When it's on, hitting the commit button will instantly upload your changes. If it's off (which it should be), you'll have a chance to review your commits before publishing them.
  3. This part of the window shows which files have been changed since the last commit. If a file is checked, it will be included in the commit you're working on. If no files are checked, you can't commit.
  4. This section shows exactly what changes have been made to the file. The line in red (also marked with `-`) was removed, and the line in green (`+`) has been added.

Also note that there are two text boxes for describing the commit. You should think of these like the fields in an e-mail: a short space for the subject, and a larger space for the body. It's a good idea to include a bit of context, but there's no need to exhaustively describe everything you've done.

Here's what shows up in the lower left of the window after I hit the "Commit" button:

<center> ![Unsynced Commits](unsynced_commits.png) </center>

Assuming the "Commit & Sync" button is turned off, you can stack commits here for as long as you like without affecting the actual site. Once you're ready to publish, hit that "Sync" button, which will do three things:

  1. Update your copy of the repository by downloading any changes that have been made since the last time you synced. (The command for this is `git fetch`)
  2. Apply your commits to the newly-updated `master` branch. (`git rebase upstream/master`)
  3. Upload your version of the repository, which now includes the changes you've made. (`git push upstream master`)

Don't panic if the above steps don't mean that much to you right now; the most important thing to know about the sync operation is that it does what it says -- synchronizes your copy with the remote copy.

## When and how to branch

The above workflow will work pretty well for quick changes, but it makes it pretty much impossible to work on multiple things at once. In real life, you'll probably have a one or two long-running projects that you'll work on regularly, polishing drafts and trying things out that you don't necessarily want to publish to the world.

You could just hold off on pushing your commits, but then what if you need to fix something else on the site? You'll have to make a new commit for that, then when you hit that "Sync" button all of your draft content will go live. Not good.

So we create **branches** for anything that's likely to take more than a commit or two to get done. Starting a new branch is sort of like using "Save as..." to begin working on an alternate version of a project. Once you've made some changes, you can decide whether to **merge** it with the `master` branch.

The process of creating branches in the GitHub app is fairly straightforward:

![Branching](branching.png)

  1. The "+" button here creates a new branch. Make sure that you start from `master` unless you have a good reason not to.
  2. Choose a descriptive name for your branch.
  3. The word "published" in this context means that your branch has been uploaded to github.com; *not* that it's live at docs.puppetlabs.com. This is an important distinction. The site is always built from the `master` branch.

Once you've set the current branch to something other than `master`, you're free to commit draft content without worrying about it showing up on the site. If/when you do want to [make one-off changes](#making-one-off-changes), just switch back to the `master` branch and go for it.

## Merging

As great as alternative branches are, they're not worth a whole lot if you don't **merge** them into `master` eventually. The GitHub app has a handy "Merge View" that looks like this:

![Merge View](merge_view.jpg)

  1. The "Merge View" button is available at the top of the Branches tab. Drag `master` into the empty space on the right and the branch that has your work into the space on the left.
  2. Make sure that this part says "Merging \<YOUR BRANCH\> into master." Also, note the semantics here: "This will merge 2 commits." As usual, the commits are what git really cares about.

When you perform the merge, git will take all of the commits from your alternate branch and pile them onto `master`, almost as if you had made them there in the first place. That means you'll have to head over to the "Changes" tab to finish the process.

That's it! The GitHub app can get you through most of your daily work here, but its simplified interface cuts both ways. As soon as things start to get even a little gnarly (and they will, sooner or later), you're going to need to drop into the terminal. Learning the core concepts and commands that underly the shiny UI will make your life *much* more pleasant when that happens.
