### Start of Development - clone the repository
```
git clone https://github.com/catan123/DeliverIT-PHP.git
```
###Setting Some Configuration Parameter for the Clone
See: http://git-scm.com/docs/git-config

```
git config user.name "Your Name"
git config user.email "your.name@rocket-internet.de"

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
git checkout -b TML-123 # same as "git checkout --track -b DMA-123 origin/DMA-123", if a local branch does not exists with this name yet but a remote one does then git creates the local branch and tracks them automatically to it
```
--track ensures the local and the remote branches are connected, so 'merge', 'pull' and 'push' sync them in both directions. 

-b ensures the creation of the local branch.
#### Commit your work
1. Update branch
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
2. Commit locally
```
# Always check the current branch and status
git status
# Add the files you want to commit
git add src/library/...
# Commit the modifications
git commit
```
3. Push changes to remote
```
# Always check the current branch and status
git status
  Your branch is ahead of 'origin/TML-123' by 1 commit
# Push only your branch modifications
git push origin TML-123
# Or push all modified branches
git push
```
4. Merge the latest master
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
5. 


