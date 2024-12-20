#### Installation:
Check installed version:
```shell
git --version
```
Install Git:
```shell
sudo apt install git
```
#### General lookups:
```shell
git ls-tree -r <branch name> #show files tracked in the repo for this branch
```
#### Git user config:
- This info is used for each commit
- Should be the same info that we have on [[GitHub]]
```shell
# Configure the Git username:
git config --global user.name "<Your GitHub Username>"
# Configure the Git email:
git config --global user.email "<Your GitHub email>"
# Check config:
git config --list
```
> We use 'global' to set the username and email for every repository on the machine.
> If you want to set the username/email for just the current repo, you can remove 'global'

#### Initialise local Git repo:
Create a project folder (a repository):
```shell
mkdir example_project #uses any normal folder, basically
cd example_project #enter the created folder

git init #register and enable current folder as a git repo
```
> Optionally allows you to attach a folder path as parameter.
> Creates a hidden folder, ".git" where the changes to the folder will be tracked.

#### Workflow:
```shell
git status #shows current branch, commits and tracked files (red files are in workspace, green files are in staging)

# ADD: (Into Staging)
git add <filename> #adds file to staging to track
git add --all #adds all files (alternatively, -A)
git add . #adds current folder and deeper (will ignore hidden files)

# COMMIT: (Staging to Local Repo)
git commit -m "<commit message>" #"m" means "message"
git log #shows commit history

# ADD & COMMIT:
git commit -am "<commit message>" #adds and commits in one command

git restore --staged new.txt #remove the added new.txt from staging

```
Files in Git repo can have 2 states:
1. Tracked - files that git knows about and are added to the repo
	- Only files added to the staging environment are tracked
2. Untracked - files in working directory, but not added to the repo
	- You can use the *".gitignore"* file (at project root folder) to keep files untracked and out of the repo. (NB: .gitignore must also be added for it to work.)
	- [[Visual Studio Code]] will show untracked files in grey.
	- Useful site for generating custom .gitignore files:
		- https://www.toptal.com/developers/gitignore
#### Branching & Merging:
```shell
git branch #list all branches (the * indicates the currently active one)
git branch <name of the branch> #create new branch from current branch
git checkout <name of the branch> #switch to branch
git checkout -b <name of the branch> #create new from current AND switch to new branch
git merge <name of branch> #merges from that branch into current branch.
git branch -d <name of branch> #deletes the branch (e.g: do it after a merge)
```
> After this command, VS Code will open conflicting files in compare mode.
> After resolving the conflicts (your edits update the currently active branch's files), you can add and commit these files to your active branch to complete the merge process.

#### GitHub:
[[GitHub]] also has a link to this section.
```shell
#Create remote repo:
	#do manually on website
	
#Clone repo to local:
git clone <URL> #Creates a subfolder, does a git init in it and loads the URL repo to that subfolder. (Will prompt credentials when private repo.)

#Push local repo to GitHub (already cloned from GitHub)
git push #Will definitely prompt for GitHub credentials, if not prompted yet

#Link local repo to GitHub repo: (NB: Must have the same name)
git remote add origin <URL> #set remote origin (the new source of truth)
	#how to see the URL afterwards:
	git remote show origin
git branch -M <branchname> #set default branch
git pull --rebase origin <branchname> #merges the local and central repo
	#when conflicts needed resolving, make the changes, then:
	git commit -am "myfixes"
	git rebase --continue #then do the push after this
		# alternatively, run:
		git rebase --abort #if you want to fully cancel the rebase
git push -u origin <branchname> #push branch to remote
	# When pushing a new branch:
	git push --set-upstream origin <branchname>

#get all remote branches into local:
for branch in `git branch -r | cut -d '/' -f2-` ; do git checkout $branch && git pull origin $branch ; done
