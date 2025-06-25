```
git init                                # Initialize a new Git repository in the current directory
git clone <repo_url>                    # Clone an existing repository from a remote source

git status                              # Check the status of the working directory (modified, staged, untracked files)
git config --global user.name "Your Name"  # Set up your global Git username
git config --global user.email "your@email.com"  # Set up your global Git email

git add <file>                          # Stage a specific file for commit
git add .                               # Stage all modified and new files
git commit -m "Your commit message"      # Commit staged changes with a message
git commit --amend -m "Updated commit message"  # Modify the last commit message

git branch                              # List all branches
git branch <branch_name>                # Create a new branch
git checkout <branch_name>              # Switch to an existing branch
git switch <branch_name>                # Alternative to checkout for switching branches
git checkout -b <new_branch>            # Create and switch to a new branch
git switch -c <new_branch>              # Alternative to create and switch to a new branch

git push origin <branch_name>           # Push the branch to the remote repository
git pull origin <branch_name>           # Fetch and merge the latest changes from the remote branch
git fetch origin                        # Fetch the latest changes from the remote without merging

git merge <branch_name>                 # Merge another branch into the current branch
git rebase <branch_name>                # Reapply commits from the current branch onto another branch
git cherry-pick <commit-hash>           # Picks a specific commit from one branch and applies it to another

git reset --soft HEAD~1                 # Undo the last commit but keep changes staged
git reset --hard HEAD~1                 # Undo the last commit and discard changes permanently
git restore <file>                      # Discard changes in a file (before staging)
git checkout -- <file>                  # Alternative to restore (older command)
git revert <commit_hash>                # Create a new commit that undoes a specific commit

git stash                               # Save uncommitted changes for later
git stash pop                           # Apply the last stashed changes
git stash list                          # View all stashed changes
git stash drop                          # Remove the last stashed change

git branch -d <branch_name>             # Delete a local branch (only if merged)
git branch -D <branch_name>             # Force delete a local branch
git push origin --delete <branch_name>  # Delete a remote branch
git rm <file>                           # Remove a file from the working directory and stage the deletion

git remote -v                           # List remote repositories
git remote add origin <repo_url>        # Add a remote repository
git remote remove origin                # Remove a remote repository

git log                                 # View commit history
git log --oneline --graph --decorate --all  # Compact history with branches
git diff                                # Show unstaged changes
git diff --staged                       # Show changes that are staged
git show <commit_hash>                  # Show details of a specific commit

git tag <tag_name>                      # Create a lightweight tag
git tag -a <tag_name> -m "Tag message"   # Create an annotated tag
git push origin <tag_name>              # Push a tag to the remote repository

git clean -f                            # Remove untracked files
git reset --hard HEAD                   # Reset to the last commit and remove all changes

git config --global alias.st "status"   # Git Alias

git reset --hard HEAD~1    # Remove last commit and discard all changes  
git reset --soft HEAD~1    # Remove last commit but keep changes unstaged  
git reset --mixed HEAD~1   # Remove last commit but keep changes staged  
git revert HEAD            # Create a new commit that undoes the last commit
```
