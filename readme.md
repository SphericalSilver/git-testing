# Git and Github - The full course

0. `git status` - Used to show current branch, current changes, untracked files, etc.
1. `git add` - Used to add files to staging area so they're included when next commit is made.
   - `git add .` - Used to add all files to staging area.
2. `git reset .` Used to undo git add.
3. `git commit -m "initial commit"` - Commits the staged changes to the branch we're working on.
4. `git log` - Shows history of commits, including author, commit id, and the branch. Note that HEAD refers to the most current commit on a given branch.
5. `git commit -a -m "Committing all changes"` - Commits all changes directly without needing to run `git add` first.
