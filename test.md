### Start of Development - clone the repository
```
git clone https://github.com/catan123/DeliverIT-PHP.git
```
###Setting Some Configuration Parameter for the Clone
See: http://git-scm.com/docs/git-config

```
git config user.name "Your Name"
git config user.email "your.email@gmail.com"

# prevent pushing all locally modified branches if the branch to push is not specified while 'git push'
git config push.default nothing
 
# Ignoring filemode changes for git calculation of file-is-modified
git config core.filemode false
```
For Windows users having their clone in the Dev-VM:
```
git config core.filemode false
git config core.autocrlf input
```
### Working with the local repository
#### Checkout a new branch
```
# Switch always to 'master' first
git checkout master
git pull
# Create the new branch
git checkout -b DMA-123
 
# When you want to push the branch remotely
git push origin DMA-123
```
#### Checkout an existing remote branch
First we can list all the branches (-a shows also the remote ones), and then checkout the branch we need (checkout will switch to the just created branch).
```
git branch -a
git checkout -b DMA-123 # same as "git checkout --track -b DMA-123 origin/DMA-123", if a local branch does not exists with this name yet but a remote one does then git creates the local branch and tracks them automatically to it
```
--track ensures the local and the remote branches are connected, so 'merge', 'pull' and 'push' sync them in both directions. 

-b ensures the creation of the local branch.
#### Commit your work
i. Update branch
```
# Check the branch you are in
git branch
  DMA-123
  * DMA-456
# If you are in another branch, switch to your
git checkout DMA-123
# Update it
git pull
```
ii. Commit locally
```
# Always check the current branch and status
git status
# Add the files you want to commit
git add src/library/...
# Commit the modifications
git commit
```
iii. Push changes to remote
```
# Always check the current branch and status
git status
  Your branch is ahead of 'origin/DMA-123' by 1 commit
# Push only your branch modifications
git push origin DMA-123
# Or push all modified branches
git push
```
iv. Merge the latest master
```
# Retrieve the latest information from remote repository
git fetch
 
# Update local master
git checkout master
git pull
 
# Merge 'master' in your branch
git checkout DMA-123
git merge master
 
# If there are conflicts, resolve them
# via Text Editor, then commit the merge
git commit -a
```
v. Rebase commits
```
git rebase -i master # combines all commits which are just in the branch and not in the master
# first commit should be 'pick', all the other ones should be 'squash'
 
# optional: if you have to resolve conflicts, fix them, git add the resulted file, and 
vim <file-to-fix>
git rebase --continue # in case merge conflict did happen, you have resolved and want to continue
 
# run now the integration tests again before you push your branch to github
 
# forces the push off the local branch to remote repository by overwriting with local commits
git push origin <branch> --force
```
vi. Squash the Pull Request
_You should always try to use rebase first instead of squashing. Only if you have to many commits mixed with master merges squashing is an alternative!_
```
# create a new branch for squashing into (starting from latest master)
git checkout master
git pull
git checkout -b <local-squash-branch>    # <local-squash-branch> could be whatever you want
 
# squash your branch into
git merge --squash <original-remote-branch>
 
# Your files are merged, but not committed yet:
# 1) Solve any conflict in your code (if there are any, check with 'git status')
# 2) Run the unit and integration tests
# Finally you can commit the squashed result
git commit -a -m "DMA-123: Ticket description"    # ATTENTION: this commit message will appear in the master!! and make sure the '-a' is present as argument
 
# do a force push to the <original-remote-branch>
git push --force origin <local-squash-branch>:<original-remote-branch>
 
# clean up your local git repo
git checkout master
git branch -D <local-squash-branch>
```

