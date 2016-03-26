
## Git Introducation 

##Trees

Tree is an object, which represents a directory. 
It holds blobs as well as other sub-directories. 
A tree is a binary file that stores references to blobs and trees which are also named as SHA1 hash of the tree object

##Commits 

Commit holds the current state of the repository. A commit is also named by SHA1 hash


##Branches
Branches are used to create another line of development. By default, Git has a master branch, which is same as trunk in Subversion. 
Usually, a branch is created to work on a new feature. Once the feature is completed, it is merged back with the master branch and we delete the branch. 
Every branch is referenced by HEAD, which points to the latest commit in the branch. Whenever you make a commit, HEAD is updated with the latest commit.

##Tags
Tag assigns a meaningful name with a specific version in the repository. Tags are very similar to branches, but the difference is that tags are immutable. 
It means, tag is a branch, which nobody intends to modify. Once a tag is created for a particular commit, even if you create a new commit, it will not be updated.
Usually, developers create tags for product releases.


##Clone
Clone operation creates the instance of the repository. Clone operation not only checks out the working copy,
but it also mirrors the complete repository. Users can perform many operations with this local repository. 
The only time networking gets involved is when the repository instances are being synchronized.

##Pull
Pull operation copies the changes from a remote repository instance to a local one. 
The pull operation is used for synchronization between two repository instances. This is same as the update operation in Subversion.

##Push
Push operation copies changes from a local repository instance to a remote one. 
This is used to store the changes permanently into the Git repository. This is same as the commit operation in Subversion.

##HEAD
HEAD is a pointer, which always points to the latest commit in the branch. Whenever you make a commit, 
HEAD is updated with the latest commit. The heads of the branches are stored in .git/refs/heads/ directory.

		[CentOS]$ ls -1 .git/refs/heads/
		master

		[CentOS]$ cat .git/refs/heads/master
		570837e7d58fa4bccd86cb575d884502188b0c49
##Revision
Revision represents the version of the source code. Revisions in Git are represented by commits. These commits are identified by SHA1 secure hashes.

##URL
URL represents the location of the Git repository. Git URL is stored in config file.

		[tom@CentOS tom_repo]$ pwd
		/home/tom/tom_repo

		[tom@CentOS tom_repo]$ cat .git/config
		[core]
		repositoryformatversion = 0
		filemode = true
		bare = false
		logallrefupdates = true
		[remote "origin"]
		url = gituser@git.server.com:project.git
		fetch = +refs/heads/*:refs/remotes/origin/*

### initial Git Client Setting  

This information is used by Git for each commit.
          
		1)Used to Set user name  
		git config --global user.name "Rupesh Shewalkar" 
		
		2)Used to Set email ID 
		git config --global user.email "shewalkar.rupesh@gmail.com"
		
		3)You pull the latest changes from a remote repository, and if these changes are divergent, then by default Git creates merge commits. 
		  We can avoid this via following settings.
		
		git config --global branch.autosetuprebase always
		
		4)The following commands enable color highlighting for Git in the console.
		
		git config --global color.ui true
		git config --global color.status auto
		git config --global color.branch auto
		
		5) Set default editor
		git config --global core.editor vim
		
		6)Git does not provide a default merge tool for integrating conflicting changes into your working tree. We can set default merge tool by enabling following settings
		git config --global merge.tool vimdiff
		
		7)Listing Git settings
		
		git config --list
		
		The above command will produce the following result.

			user.name=Rupesh Shewalkar
			user.email=shewalkar.rupesh@gmail.com
			push.default=nothing
			branch.autosetuprebase=always
			color.ui=true
			color.status=auto
			color.branch=auto
			core.editor=vim
			merge.tool=vimdiff

## Git commands
		
		1)used to git initialize
		  git init
		  
		2)shows status 
		git status 
		
		3)Used to add files in repo
		
		git add .  
		
		4)Used to commit the changes
		git commit -m "First commit"
		
		5)shows logs 

	        git logs
		
		6) Add Remote git repo 
		git remote add origin git@github.com:rupeshshewalkar/Dockerfile.git  
		
		7) Used to push contents into remote master branch
		git push origin master 
		
		8)Used to clone remote contents into local
		
		git clone git@github.com:rupeshshewalkar/Dockerfile.git 
		
		9)git show command to view the commit details.
		git show 
		
		10)Used pull contents from remote to local
		git pull 
		
		11) Used to rename file1 to file2 
		git mv file1 file2   
		
		12) Used to remove file 
		git rm file2  
		
		13) View remote urls
                git remote -v 
		
		14) Change origin url
		git remote set-url origin http//github.com/repo.git   
		
		15) Add remote
		git remote add remote-name https://github.com/user/repo.git  
		
		16) See non-staged (non-added) changes to existing files
		git diff
		Note that this does not track new files.

		17) See staged, non-commited changes
		git diff --cached
		
		16) See differences between local changes and master
		git diff origin/master
		Note that origin/master is one local branch, a shorthand for refs/remotes/origin/master, which is the full name of the remote-tracking branch.

		18) See differences between two commits
		git diff COMMIT1_ID COMMIT2_ID
		
		19) See the files changed between two commits
		git diff --name-only COMMIT1_ID COMMIT2_ID
		
		20) See the files changed in a specific commit
		git diff-tree --no-commit-id --name-only -r COMMIT_ID
		or

		git show --pretty="format:" --name-only COMMIT_ID
	

		21) See diff before push
		git diff --cached origin/master
		
		
		22) See commit history for the last two commits
		git log -2
		
		23) See commit history for the last two commits, with diff
		git log -p -2
		
		24) See commit history printed in single lines
		git log --pretty=oneline
		
		25) Revert one commit, push it
		git revert dd61ab21
		git push origin master
		
		26) Revert to the moment before one commit
	            # reset the index to the desired tree
		
		git reset 56e05fced

		27) move the branch pointer back to the previous HEAD
		git reset --soft HEAD@{1}

		git commit -m "Revert to 56e05fced"

		28) Update working copy to reflect the new commit
		git reset --hard
		
		29) Undo last commit, preserving local changes
		git reset --soft HEAD~1
		
		30) Undo last commit, without preserving local changes
		git reset --hard HEAD~1
		
		31) Undo last commit, preserving local changes in index
		git reset --mixed HEAD~1
		Or git reset HEAD~1
		
		32) Undo non-pushed commits
		git reset origin/master
		
		33) Reset to remote state
			git fetch origin
			git reset --hard origin/master
			
		34) See local branches
		git branch
		
		35) See all branches
		git branch -a
		
		
		36) Make some changes, create a patch
		git diff > patch-issue-1.patch
		
		37) Add a file and create a patch
		git add newfile
		git diff --staged > patch-issue-2.patch
		
		38) Add a file, make some changes, and create a patch
		git add newfile
		git diff HEAD > patch-issue-2.patch
		
		39) Make a patch for a commit
		git format-patch COMMIT_ID
		
		40) Make patches for the last two commits
		git format-patch HEAD~2
		
		41) Make patches for all non-pushed commits
		git format-patch origin/master
		
		42) Create patches that contain binary content
		git format-patch --binary --full-index origin/master
		
		43) Apply a patch
		git apply -v patch-name.patch
		
		44) Apply a patch created using format-patch
		git am patch1.patch
		
		45)Create a branch
		git checkout master
		git branch new-branch-name
		Here master is the starting point for the new branch. Note that with these 2 commands we don't move to the new branch, as we are still in master and we would need to run git checkout new-branch-name. The same can be achieved using one single command: git checkout -b new-branch-name

		46)Checkout a branch
		git checkout new-branch-name
		
		47)See commit history for just the current branch
		git rupesh -v master
		(master is the branch you want to compare)

		48)Merge branch commits
		git checkout master
		git merge branch-name
		Here we are merging all commits of branch-name to master.

		49)Merge a branch without committing
		git merge branch-name --no-commit --no-ff
		
		50)See differences between the current state and a branch
		git diff branch-name
		
		51)See differences in a file, between the current state and a branch
		git diff branch-name path/to/file
		
		52)Delete a branch
		git branch -d new-branch-name
		
		53)Push the new branch
		git push origin new-branch-name
		
		54)Get all branches
		git fetch origin
		
		55)Get the git root directory
		git rev-parse --show-toplevel
		
		56)Remove from repository all locally deleted files
		git rm $(git ls-files --deleted)
		
		57)Delete all untracked files
		git clean -f
		Including directories:
		git clean -f -d
		
		58)Unstage (undo add) files:
		git reset HEAD file.txt

##Git - Stash Operation

Suppose you are implementing a new feature for your product. Your code is in progress and suddenly a customer escalation comes. 
Because of this, you have to keep aside your new feature work for a few hours. You cannot commit your partial code and also cannot throw away your changes. 
So you need some temporary space, where you can store your partial changes and later on commit it.

In Git, the stash operation takes your modified tracked files, stages changes, and saves them on a stack of unfinished changes that you can reapply at any time.

			root@vagrant-ubuntu-trusty-32:~/github/Dockerfile# git status -s
			M README.md

Now, you want to switch branches for customer escalation, but you don’t want to commit what you’ve been working on yet; so you’ll stash the changes. To push a new stash onto your stack, run the git stash command.

			root@vagrant-ubuntu-trusty-32:~/github/Dockerfile# git stash
			Saved working directory and index state WIP on master: 525fd08 Gnowsis Project Upload
			HEAD is now at 525fd08 Gnowsis Project Upload

Now, your working directory is clean and all the changes are saved on a stack. Let us verify it with the git status command.

			root@vagrant-ubuntu-trusty-32:~/github/Dockerfile# git status
			On branch master
			nothing to commit, working directory clean

Now you can safely switch the branch and work elsewhere. We can view a list of stashed changes by using the git stash list command.

			root@vagrant-ubuntu-trusty-32:~/github/Dockerfile# git stash list
			stash@{0}: WIP on master: 525fd08 Gnowsis Project Upload

Suppose you have resolved the customer escalation and you are back on your new feature looking for your half-done code, just execute the git stash pop command, to remove the changes from the stack and place them in the current working directory.

			root@vagrant-ubuntu-trusty-32:~/github/Dockerfile# git stash pop
			On branch master
			Changes not staged for commit:
			  (use "git add <file>..." to update what will be committed)
			  (use "git checkout -- <file>..." to discard changes in working directory)

					modified:   README.md

			no changes added to commit (use "git add" and/or "git commit -a")
			


			
			
## Tags

Tag operation allows giving meaningful names to a specific version in the repository.

Branches

If you think of your repository as a book that chronicles progress on your project...
You can think of a branch as one of those sticky bookmarks.
A brand new repository has only one of those (called master), which automatically moves to the latest page (think commit) you've written. However, you're free to create and use more bookmarks, in order to mark other points of interest in the book, so you can return to them quickly.
Also, you can always move a particular bookmark to some other page of the book (using git-reset, for instance); points of interest typically vary over time.

Tags
You can think of tags as chapter headings
It may contain a title (think annotated tags) or not. A tag is similar but different to a branch, in that it marks a point of historical interest in the book.
Note that, once you've shared a tag (i.e. pushed it to a shared remote), you're not supposed to move it to some other place in the book.


## Tag demostration 
		
			root@vagrant-ubuntu-trusty-32:~#mkdir sand-box
			root@vagrant-ubuntu-trusty-32:~#cd sand-box/
			root@vagrant-ubuntu-trusty-32:~#git init
			Initialized empty Git repository in /root/sand-box/.git/
			
			root@vagrant-ubuntu-trusty-32:~/sand-box# ll
			total 12
			drwxr-xr-x 3 root root 4096 Mar 26 03:57 ./
			drwx------ 6 root root 4096 Mar 26 03:57 ../
			drwxr-xr-x 7 root root 4096 Mar 26 03:57 .git/

			root@vagrant-ubuntu-trusty-32:~/sand-box# touch index.html
			
			root@vagrant-ubuntu-trusty-32:~/sand-box# git add .
			root@vagrant-ubuntu-trusty-32:~/sand-box# git commit -m "initial commit"
			[master (root-commit) 71ca410] initial commit
			 1 file changed, 0 insertions(+), 0 deletions(-)
			 create mode 100644 index.html
			
			root@vagrant-ubuntu-trusty-32:~/sand-box# git tag
			root@vagrant-ubuntu-trusty-32:~/sand-box# git tag v0
			root@vagrant-ubuntu-trusty-32:~/sand-box# git tag
			v0
			root@vagrant-ubuntu-trusty-32:~/sand-box# vi index.html
			root@vagrant-ubuntu-trusty-32:~/sand-box# git add .
			root@vagrant-ubuntu-trusty-32:~/sand-box# git status
			On branch master
			Changes to be committed:
			  (use "git reset HEAD <file>..." to unstage)

					modified:   index.html

			root@vagrant-ubuntu-trusty-32:~/sand-box# git commit -m " commit on index.html"
			[master d4608a0]  commit on index.html
			 1 file changed, 5 insertions(+)
			root@vagrant-ubuntu-trusty-32:~/sand-box# git status
			On branch master
			nothing to commit, working directory clean
			root@vagrant-ubuntu-trusty-32:~/sand-box# git tag
			v0
			root@vagrant-ubuntu-trusty-32:~/sand-box# git tag v1
			root@vagrant-ubuntu-trusty-32:~/sand-box# git tag
			v0
			v1
			root@vagrant-ubuntu-trusty-32:~/sand-box# cat index.html
			<html>
			<body>
			<h1> version1</h1>
			</body>
			</html>
			root@vagrant-ubuntu-trusty-32:~/sand-box# git checkout v0
			Note: checking out 'v0'.

			You are in 'detached HEAD' state. You can look around, make experimental
			changes and commit them, and you can discard any commits you make in this
			state without impacting any branches by performing another checkout.

			If you want to create a new branch to retain commits you create, you may
			do so (now or later) by using -b with the checkout command again. Example:

			  git checkout -b new_branch_name

			HEAD is now at 71ca410... initial commit
			root@vagrant-ubuntu-trusty-32:~/sand-box# cat index.html
			root@vagrant-ubuntu-trusty-32:~/sand-box# git checkout v1
			Previous HEAD position was 71ca410... initial commit
			HEAD is now at d4608a0...  commit on index.html
			root@vagrant-ubuntu-trusty-32:~/sand-box# cat index.html
			<html>
			<body>
			<h1> version1</h1>
			</body>
			</html>




