# Git and Github - The full course

Git refresher by fireship.io. Informative course! Really helpful notes.

## General Notes

Link to repo: https://github.com/SphericalSilver/git-testing.git

3 Different File directories of Git:

- Working Directory (Contains files you're looking at in VScode)
- Staging Area (created on git add)
- Commits (Commit history)

0. `git status` - Used to show current branch, current changes, untracked files, etc.
1. `git add` - Used to add files to staging area so they're included when next commit is made.

   - `git add .` - Used to add changes to staging area, including new files. (but not file deletions).
   - `git add -u` or `git add --update` - Stages new files and modifications and deletions (without new files)
   - `git add -A` or `git add --all` which stage ALL changes, including file deletions, new files, etc. This is equivalent to both the above commands.

2. `git commit -m "initial commit"` - Commits the staged changes to the branch we're working on.
3. `git log` - Shows history of commits, including author, commit id, and the branch. Note that HEAD refers to the most current commit on a given branch.
4. `git commit -a -m "Committing all changes"` - Commits all changes directly without needing to run `git add` first.
   - `git commit -am "Committing all changes"` - This equivalent to the above (to double check)
5. `git remote` - Tells us which remote repositories we have linked.
6. `git remote add origin https://github.com/SphericalSilver/git-testing.git` - Connects local code to a remote repo. Replace `origin` with name of remote repository (usually it's origin, as it's main source of truth for code). The argument after that is the URL to that remote repository (usually copied from github).
7. `git remote -v` - Shows URL to remote repo.
8. `git remote show origin` - Shows URL along with other info like the branches.
9. `git push origin master -u` - Uploads code from local repo to remote repo. Last 2 arguments are name of remote repo (origin), and the branch we are pushing (master, in this example). The -u sets the origin repo to the upstream remote in the git config file. Essentially, we use the -u flag when the remote repository is the final source of truth.
10. `git fetch` - Downloads latest changes from remote repo. After this, merging still needs to be done.
11. `git merge origin/master` - Last argument is the branch we are merging on top of the branch that we're currently locally on. In this case, the master branch from the remote repo is being merged into our local branch which we're on.
12. `git pull origin master` - Combines `git fetch` and `git merge`. If the `-u` flag was given during `git push`, the last 2 arguments are not needed (i.e. just `git pull` would work.) Note that if you have uncommitted changes in your local changes, git pull won't work. So either commit the changes, or stash them.
13. `git clone <url here>` - Clones a repo to the local.
14. `git branch` - Lists all branches in the current project.
15. `git branch -M main` - renames current branch to last parameter (main)
16. `git branch awesome` - Creates a branch using the name of the last parameter (awesome)
17. `git branch -d awesome` - Deletes the branch "awesome" (Lowercase d makes it so the deletion only takes place when the branch hasn't been merged to master branch. Replacing it with uppercase d will cause the deletion to go through no matter what.)
18. `git checkout awesome` - Changes current working branch to the "awesome branch".

- If you checkout a new branch, and then make changes there and commit them, when you switch to any other branch, those changes should disappear as they were only there on that branch.
- `git checkout -` - Brings you to previous branch (in case you forgot its name, this might be a helpful shortcut.)
- `git checkout -b feature` - Creates a new branch called "feature" and brings you to it.

20. `git diff` - To see changes between conflicting git branches.

- `git merge --abort` - Takes us back to the original state before a merge was started. Should be used to figure out how to handle merge conflicts.
- The easiest way to fix the merge conflict is use the editor to choose between the incoming changes (feature) or the existing changes (master). Then create a new merge commit on the current branch with the changes made, and then try to merge again.

21.

## Stash

Used for saving changes that you don't want to commit. The stash is like an array which holds on to changes you want to apply later.

1. `git stash` - Stashes changes.
2. `git stash save <name1>` - Applies `git stash`, but when you do `git stash list`, you'll see a list of the stashes saved. This is useful if you want to split your stashes. `name1` here is the name of that stash that will show.
3. `git stash list` - Lists all stashed changes by their name and index (0-indexed)
4. `git stash pop` - Applies most recently stashed change.
5. `git stash apply 1` - Applies the stash based on its index

## Rebasing and Squashing

In a team, rebasing is often used in place of merging. Rebasing makes it so that if you're working on a feature branch, the most recent changes from the master branch are applied, as though that was the branch you were originally working from in the first place. This should only be done on private feature branches you're working on due to the destructive way in which it "rewrites" history.

This is a really useful way to keep feature branch up to date with master branch. In contrast, while merging may achieve a similar goal, it would add a lot of commits unnecessary, causing clutter.

1. `git rebase master` - Used from the feature branch. It takes the feature branch, and puts it on the tip of the `master` branch. Makes it look like you just began working on this feature with the latest code from the master branch.

- If you're unsure about doing a rebase, you can create an extra branch from your current feature, then do a rebase (from master` on that branch to sense-check that everything works out okay. If it does, then rebasing the original feature branch should work too.

2. `git rebase master --interactive` - Start an interactive rebase from a feature, then choose the squash command to flatten your commits into a single message. Replace "pick" with "squash" for the later commits, to squash them so that they only show as a single commit. Save the interactive file then close it, and then when another file opens up that prompts you to edit the commit message, close that new file too. Squashing is usually the last thing you do before doing a Pull Request or merge the feature back into the master branch.

## Resetting, reverting, amending.

2. `git reset .` - Used to undo git add.
3. `git reset <commit_id>` - Used when you want to reverse a commit (last argument is commit_id, which you can find using git log). Using git log again will show that the head of the branch is now that new commit. This won't automatically undo all changes, you'll still need to make the manual fixes and then recommit them. Note that you should never do a reset when the commit has already been pushed to a remote repository, as other developers may already be relying on it.
4. `git reset --hard <commit_id>` - Deletes the committed changes from that commit_id, have to be careful when using this.
5. `git revert <commit_id>` - Reverts the changes made from the commit_id specified. The bad commit isn't actually lost though, it will still be in history. There will be another commit created that will have been responsible for reverting the bad one - this commit can then be pushed to the remote repo. When working with a remote repo, this is preferable to git reset for the reason that it doesn't hard delete the bad commit. `git reset` is best reserved for when working locally only.
6. `git commit --amend -a "new commit message"` - Updates the last commit message
7. `git commit --amend --no-edit` - Used to update a commit without changing the last commit message (maybe you made some changes you wanted to make, or there were files you didn't stage yet and you just staged them.) The advantage of this over `git revert` is that an extra commit isn't created.

## Forking

- Forking can be used to create a version of a repository in your own gitlab account, while maintaining a link to the original, such that it can fetch updates from the upstream repository
- Often develops may fork a repo, and then clone that forked version on their local machine to and then work there to, for instance, build a new feature, then make a pull request for the author of the original repo to decide whether they want to accept that pull request.
- Pull requests have to be made from the github or gitlab console.
- `git remote add upstream https://github.com/fireship-io/git-sticker.git` - Add a remote link to the upstream repo (original repo)
- `git fetch upstream` - Downloads latest changes from remote repo.
- `git rebase upstream/master` - Adds changes from the upstream remote repository onto the local branch.
