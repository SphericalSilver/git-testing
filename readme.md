# Git and Github - The full course

Git refresher by fireship.io

Link to repo: https://github.com/SphericalSilver/git-testing.git

0. `git status` - Used to show current branch, current changes, untracked files, etc.
1. `git add` - Used to add files to staging area so they're included when next commit is made.
   - `git add .` - Used to add changes to staging area, including new files. (but not file deletions).
   - `git add -u` or `git add --update` - Stages new files and modifications and deletions (without new files)
   - `git add -A` or `git add --all` which stage ALL changes, including file deletions, new files, etc. This is equivalent to both the above commands.
2. `git reset .` - Used to undo git add.
3. `git commit -m "initial commit"` - Commits the staged changes to the branch we're working on.
4. `git log` - Shows history of commits, including author, commit id, and the branch. Note that HEAD refers to the most current commit on a given branch.
5. `git commit -a -m "Committing all changes"` - Commits all changes directly without needing to run `git add` first.
   - `git commit -am "Committing all changes"` - This equivalent to the above (to double check)
6. `git remote` - Tells us which remote repositories we have linked.
7. `git remote add origin https://github.com/SphericalSilver/git-testing.git` - Connects local code to a remote repo. Replace `origin` with name of remote repository (usually it's origin, as it's main source of truth for code). The argument after that is the URL to that remote repository (usually copied from github).
8. `git remote -v` - Shows URL to remote repo.
9. `git remote show origin` - Shows URL along with other info like the branches.
10. `git push origin master -u` - Uploads code from local repo to remote repo. Last 2 arguments are name of remote repo (origin), and the branch we are pushing (master, in this example). The -u sets the origin repo to the upstream remote in the git config file. Essentially, we use the -u flag when the remote repository is the final source of truth.
11. `git fetch` - Downloads latest changes from remote repo. After this, merging still needs to be done.
12. `git merge origin/master` - Last argument is the branch we are merging on top of the branch we're currently locally on. In this case, the master branch from the remote repo is being merged into our local branch which we're on.
13. `git pull origin master` - Combines `git fetch` and `git merge`. If the `-u` flag was given during `git push`, the last 2 arguments are not needed (i.e. just `git pull` would work.) Note that if you have uncommitted changes in your local changes, git pull won't work. So either commit the changes, or stash them.
14. `git clone <url here>` - Clones a repo to the local.
15. `git branch` - Lists all branches in the current project.
16. `git branch -M main` - renames current branch to last parameter (main)
17. `git branch awesome` - Creates a branch using the name of the last parameter (awesome)
18. `git branch -d awesome` - Deletes the branch "awesome" (Lowercase d makes it so the deletion only takes place when the branch hasn't been merged to master branch. Replacing it with uppercase d will cause the deletion to go through no matter what.)
19. `git checkout awesome` - Changes current working branch to the "awesome branch".
    20 .
