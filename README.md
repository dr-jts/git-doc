# Git Commands

## Config

`git config --global user.email mtnclimb@gmail.com`

## Reporting

git diff --name-status <commit1>..<commit2>
reports files in diff between two commits.  Commits can be branch names as well
git diff --cached
diff for changes in staging area
git show <commit>
shows the contents of a commit
git log --author=mdavis --oneline
log for me in short form
git log --author=mdavis
shows log for me
git whatchanged
show files that changed in each commit

## Creating repos

git clone ~/proj/geoserver/git/geoserver geoserver
git clone ~/proj/geotools/git/geotools geotools
Clones local git repo into dir ‘geoserver’
git clone git@github.com:mdavisog/geoserver-exts.git 
git clone git@github.com:dr-jts/geotools.git 
git clone git@github.com:dr-jts/jeql.git 


clones github repo “geoserver” into current dir
git clone https://github.com/dr-jts/jeql
clones Github repo into curent dir

## Remotes

git remote add upstream git://github.com/geoserver/geoserver.git

git remote add  name   git://git-url/repo.git

git remote add name git@github.com:opengeo/geoserver-exts.git
create upstream remotes
git remote set-url --push upstream git@github.com:geotools/geotools.git 

git remote set-url --push upstream git@github.com:geoserver/geoserver.git 

git remote set-url --push origin git@github.com:dr-jts/geoserver.git
change URL for remote


git remote -v
git remote -v show <origin>
show remotes
show full info about remotes
git ls-remote <origin>
list remote refs
git remote rename from-name to-name
rename a remote
git remote rm <remote>
remove a remote


# Branches
## Show
git branch -a - show all local branches
git branch -r - show remote branches
Git branch -vv - very verbose output
  
## Rename
git branch -m <old_branch_nm> <new_branch_nm> - rename branch
## Change tracking branch
git branch branch_name -u your_new_remote/branch_name
  
## Delete

git branch -d <branch>
delete a branch ONLY if it’s merged
git branch -D <branch>
delete a branch regardless of its merge state
git push origin --delete <branch>
delete a remote branch
git fetch -p
Git fetch --prune
clean up deleted remote branches


## Checkout

git checkout -b 21x origin/2.1.x
Create a branch 21x tracking a remote branch “2.1.x”
git checkout --track origin/some_branch
Create a branch tracking remote with same name



git checkout -b <branchname> - create a new branch <branchname> and switch to it


git checkout -- <file>  -- revert particular file(s) to last committed revision

Copy a file
git checkout <otherbranch> <file> - checkout (copy) a single file from a branch into current

# Synching

git fetch origin 
git reset --hard origin/master
Reset local repository branch to mirror remote repository HEAD

# Patches

git diff master..doco > ~/http.rst.patch  - create a patch for the changes in doco relative to master, save to a file

git diff --name-only master..gcstrans - only show names of modified files

git apply <patch> - apply the patch file to the current branch (without commiting)

# Status

git status -u --ignored  - show ignored files in status

# History / Log
git log

# Adding

git add file...
git add -A file... - add all files, including deletes
git add --patch <files...> - interactively add sections of file modifications
git add --interactive - more powerful mode of above

## Committing

git commit -m “msg”
commit staged (added) files, with message
git commit -am "msg"
add/commit ALL FILES, with message
git commit --amend
squash commit into last commit
git commit --amend -m "New msg"
amend last commit message
git commit -C <commit>
commit copying message from another commit (useful when fixing  cherry-picks)

## Squashing 

git reset --soft   <commit ref>
git commit [ -m “msg” ]

Sqash commits  after <ref> into single commit

## Cherry-picking

git cherry-pick <commit>

copies commit into current branch.  If commit is clean it is added.  
If not clean, contents are added to staging/working area for fixup.  To revert use git reset --hard HEAD.  To commit with original message use git commit -C <commit>


git cherry-pick sha1^..sha2
Copies commits sha1 thru sha2 INCLUSIVE of sha1

## Pushing

git push origin
Push changes from current local branch to remote “origin” branch with same name
git push origin xxx
Push changes from local branch xxx 
to remote “origin” branch “xxx”
git push -f origin xxxx
DANGEROUS!!!
Force a push (eg of an amended commit)







Pulling
git pull origin master 
Pull changes from remote ‘origin’ branch ‘master’ into current branch
git pull upstream master
Pull changes from remote upstream branch ‘master’ into current branch
git pull --rebase upstream master
Pull changes from remote upstream branch ‘master’ into current branch, rebasing any local commits onto HEAD of master






## Fixing things
### Reset Working Area
  
`git reset --hard HEAD`
* Reset working area to HEAD
  
`git reset --hard HEAD^`
* Reset to before last commit
  
`git reset --soft HEAD^`
* Move last commit back to staging area


`git reset --soft <remote ref>`
`git reset --soft master`
* Move local back to HEAD of remote ref
  
`git reset HEAD <file>`
* Reset file from staging area into working area
  
`git reset --hard <remote ref>`
* Reset current branch to state of <remote ref>
  Common case: ref is remote/branch

`git clean -f -d`
* remove untracked files and directories from working area
 
`git clean -d -f -x`
* remove all untracked objects from working area

## Files

git checkout -- <file>  
revert particular file(s) to last committed revision


## Commits

git commit --amend -m "new msg"
Change commit message of last commit
git commit --amend
Amend last commit, adding any new files in staging area







Rebasing

git rebase -i HEAD~n
squash commits including last n commits
git rebase -i <commit #>
edit commits since <commit #>, eg to do squashing
git rebase origin/master
merge in the requested branch (origin/master in this case) and apply the commits that you have made locally to the top of the history without creating a merge commit (assuming there were no conflicts).
git rebase --abort
reverts rebase, leaving branch as it was before




Stashing
git stash
stash changes (NOTE untracked files are not stashed)
git stash list
show stash items
git stash pop
pop stashed changes back into working area
git stash apply
apply changes but don’t remove them from stash
git stash drop
deletes top stash item
git stash show [ <name> ]
shows files in stash entry
git stash show -p [ <name> ]
shows stash entry as a patch


Submodules
git submodule update [ --recursive ]
Update submodules (eg when status shows “new commits”)



















Tracking other repo

git remote add (party) (url)
git remote update
git checkout (party)/branch -b (party)-branch --track


git remote add lt https://github.com/locationtech/jts.git 
git remote add volaya git://github.com/volaya/suite.git
git remote update
git checkout volaya/master -b volaya-master --track
git pull volaya master:volaya-master

Mac Tricks
Don’t track .DS_Store

# specify a global exclusion list 
git config --global core.excludesfile ~/.gitignore 
# adding .DS_Store to that list 
echo .DS_Store >> ~/.gitignore
