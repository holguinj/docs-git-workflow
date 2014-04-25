Git Workflow for PE X or Y releases:
====================================

For this walkthrough, assume we are working on docs for the 3.3 release of PE.

1. Start by checking out public master: `git co upstream/master`
2. Make a new branch at this point: `git co -b pe3.3-dev`
3. Make the changes, additions, etc. needed for 3.3. docs to the files in the current (i.e., `3.2`) directory. Note that there is no `3.3` directory at this point, we're pretending that `3.2` is it.
4. Periodically, while on the `pe3.3-dev` branch, pull over changes from master with `git fetch upstream && git merge upstream/master`. You'll also need to resolve any merge conflicts that occur.
5.  As needed, commit and push your work up to the private repo with `git push private pe3.3-dev`. After you've done this once you can optionally do `git branch --set-upstream-to private/pe3.3-dev`. This will let you see proper git status messages and should let you just do `git push` in the future.
6. Do the same thing for the nav file in `_includes` (that is, work on the 3.2 version)
7. At release time, move the files in the `3.2` directory to a new `3.3` directory: `git mv 3.2 3.3`
8. Get a fresh copy of the `3.2` directory: `git co upstream/master 3.2`
9. Do the same thing with the nav file (rename it `3.3` and then get a fresh copy of the old `3.2` version)
10. Do `git status` to make sure all the added files and directories are green. If not, add as needed before you commit.
11. Move onto master branch with `git co master`, and make sure it is up to date with `git pull`.
12. Merge in the dev branch: `git merge pe3.3-dev`
13. Publish the work: `git push upstream master`
