# Git and Github - The full course

Link to repo: https://github.com/SphericalSilver/git-testing.git

0. `git status` - Used to show current branch, current changes, untracked files, etc.
1. `git add` - Used to add files to staging area so they're included when next commit is made.
   - `git add .` - Used to add all files to staging area.
2. `git reset .` - Used to undo git add.
3. `git commit -m "initial commit"` - Commits the staged changes to the branch we're working on.
4. `git log` - Shows history of commits, including author, commit id, and the branch. Note that HEAD refers to the most current commit on a given branch.
5. `git commit -a -m "Committing all changes"` - Commits all changes directly without needing to run `git add` first.
6. `git remote` - Tells us which remote repositories we have linked.
7. `git remote add origin https://github.com/SphericalSilver/git-testing.git` - Connects local code to a remote repo. Replace `origin` with name of remote repository (usually it's origin, as it's main source of truth for code). The value after that is the URL to that remote repository (usually copied from github).
8. `git remote -v` - Shows URL to remote repo.
9. `git remote show origin` - Shows URL along with other info like the branches.
10. `git push origin master -u` - Uploads code from local repo to remote repo. Last 2 arguments are name of remote repo (origin), and the branch we are pushing (master, in this example). The -u sets the origin repo to the upstream remote in the git config file. Essentially, we use the -u flag when the remote repository is the final source of truth.
