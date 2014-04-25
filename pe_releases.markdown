Git Workflow for PE X or Y releases:
====================================

For this walkthrough, assume we are working on docs for the 3.3 release of the PE.

1. Make sure you're starting from the most recent commit in the upstream (i.e. public) master branch: git checkout upstream/master
2. Create a new branch: git co -b pe3.3-dev
3. Set the new branch to push to private/pe3.3-dev by default: git branch --set-upstream-to private/pe3.3-dev
4. Make the changes, additions, etc. needed for 3.3. docs to the files in the current (i.e., 3.2) directory. Note that there is no 3.3 directory yet. Just pretend that 3.2 is it.
5. Periodically, while on the PE3.3-dev branch, fetch the current upstream/master and merge it in. This is when merge conflicts will show up, so you'll have to resolve them before you can continue: git fetch upstream && git merge upstream/master
6. As needed, commit and push your work up to the private repo, which should be the default after step 3: git push
7. Do the same thing for the nav file in _includes (that is, work on the 3.2 version)
8. At release time, move the files in the 3.2 directory to a new 3.3 directory with git mv 3.2 3.3
9. Get a fresh copy of the 3.2 directory with git co master 3.2
10. Do the same thing with the nav file (rename it 3.3 and then get a fresh copy of the old 3.2 version)
11. Do git status to make sure all the adds, etc. are green. If not, add and commit as needed.
12. Move onto master branch: git co master
13. Merge in the dev branch: git merge PE3.3-dev
14. Publish the work: git push upstream master
