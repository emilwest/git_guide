.. gitGuide documentation master file, created by
   sphinx-quickstart on Sun May 13 14:26:16 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

A Git Reference Guide
====================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`


General lexicon
=======

This is a glossary with definition terms for thing like :term:`origin`:

.. glossary::
	The three states
		Git has three main states that your files can reside in: committed, modified, and staged: 
			comitted
				when the data is safely stored in your local database
			modified
				you have changed the file but have not committed it to your database yet
			staged
				you have marked a modified file in its current version to go into your next commit snapshot
	snapshot
		a 'picture' of how how your files look when you commit. 
	
	commit
		[verb] the command of recording the snapshot that was set up in the staging area (with git add <files>). 
		[noun] a object with snapshot information: which branch it was comitted in, SHA-1 checksum, etc. This snapshot can be reverted or compared to later.
	
	branch
		A moveable pointer to a specific :term:`commit`. 
	
	HEAD
		tip (latest commit) of the current local branch (cat .git/HEAD). This is a pointer used for git to know which :term:`branch` you're currently on. 
	
	merge
	merging
		The process of combining the commits of one branch into the current HEAD branch. Eg: git checkout master; git merge feature-branch; will merge feature-branch into the master branch. 
	
	merge conflict
		Occurs when the same part of the same file has been modified differently in the two branches you're merging together. 
	
	
	origin
		an alias that stores the URL of the remote repository
		(see url with: git remote -v )
		(git remote show origin)
	
	remote
		refers to a repository which is a version of your project that is hosted on the Internet or network somewhere, commonly github, gitlabs, etc.
	
	

	
	

	
	

Branching
=======

.. glossary::
	
	git pull origin <branch-to-pull>
		Pull from specific branch
	
	git push <remote-name> <branch-name>
	git push origin HEAD
		Push a branch you want to share to origin. Then, on gitlabs, you can choose which branch you want to submit the merge request to.
	
	git push origin HEAD:integration
		Push local branch to a remote branch
	
	git checkout < branchname >
		switch the HEAD pointer to a different branch
		-b < branchname >: create a new branch and switch to it


pull
----

Pull from specific branch::

 git pull origin <branch-to-pull>

For example:
 git pull origin HEAD # pulls from origin (the url of the remote repository) the branch your currently on (HEAD)

 git pull origin other/branch # pulls from origin a branch called 'other/branch'


push
----

Push a branch you want to share to origin::

 git push origin <branch-name> OR git push origin HEAD

Then, on gitlabs, you can choose which branch you want to submit the merge request to.

Push local branch to a remote branch::

 git push origin HEAD:integration

checkout
--------

switch the HEAD pointer to a different branch::

 git checkout < branchname > 
Options:

-b  create a new branch and switch to it, eg: git checkout -b <branchname>


branch
------

shows a list of local branches::

 git branch

< branchname >  creates a new branch with that name:: 

  git branch <branchname>
  
Options: git branch 
-------



-d  delete a branch eg: -d <branchname>

-v  show the last commit on each local branch

-vv  see what tracking branches you have set up

-a  show local and remote branches

-va  show the last commit on each local and remote branch

--merged  list which branches are already merged into the working branch (safe to delete)

--no-merged  list which branches are not merged into the working branch. can be used to compare branches, eg. what is not merged in this branch compared to the master branch? : git branch --no-merged master

-m  rename a branch, eg: git branch -m «old branch» «new branch»

 


Remote branches
===============

.. glossary::
	
	git fetch origin
		To sync with the remote
		
	git merge origin/<branch>
		To get a local copy of the remote branch
	
	git checkout -b my_new_branch origin/<branch>
		create a new branch based origin/<branch>

Respresented as:: 

 <remote>/<branch>, eg: origin/emil_westin

If you do some work on your local master branch, and, in the meantime, someone else pushes to the remote branch,
then your histories move forward differently.

To sync with the remote, run::

 git fetch origin

This only gives a pointer to the origin/<branch>. To get a local copy, you can::

 git merge origin/<branch>

or, if you want to create a new branch based on this origin/<branch> ::

 git checkout -b my_new_branch origin/<branch>


	Branch my_new_branch set up to track remote branch <branch> from origin.
	Switched to a new branch 'my_new_branch'

 

View commit history
=======

.. glossary::
	git log [option]
		shows the detailed commit history

log
---

shows the detailed commit history::

 git log [option]

Options: 

-1  only shows the last 1 commit

-p  shows the line diff for each commit

-p --word-diff  shows the word diff for each commit

--stat  shows stats instead of diff details

--name-status  shows a simpler version of stat

--oneline  just shows commit comments

shows a nice commit tree::

 git log --oneline --all --decorate --graph 

 


Undo things
=======

.. glossary::
	git reflog
		Show previous git reference ids. Returns a <ref>, eg: c5f567
	
	git reset [option] [<ref>]
		Undo a pull or commit
	
	git commit --amend
		If you want to try the commit again, eg. include more files into the commit:  git commit -m 'initial commit' $ git add forgotten_file $ git commit --amend
	
	git commit --amend -m "new message"
		Re-write the message from last commit

reflog
------

Show previous git reference ids::

 git reflog

reset
-----

Undo a pull or commit::

 git reset --hard <ref>

Or: git reset --hard HEAD~1

Reset options:

--soft  undo last commit but changes stays in working tree (the index) so a git commit will "undo the undo".

--mixed  undo last commit but changes stays in staging area, so you'll need to add the files to commit them.

--hard  undo everything. Only use if you want to undo a pull.

Re-write the message from last commit::

 git commit --amend -m "new message"



Reverting
=======

.. glossary::
	git checkout <ref> -- file1/to/restore file2/to/restore
		Revert specific file
	
	git checkout <ref>~1 -- file1/to/restore file2/to/restore
		If you want to revert to the commit before eg. c5f567, append ~1

Revert specific file::

 git checkout <ref> -- file1/to/restore file2/to/restore

If you want to revert to the commit before c5f567, append ~1 ::

 git checkout <ref>~1 -- file1/to/restore file2/to/restore



Checkout
=======

.. glossary::
	git clean
		checkout all untracked files

clean
-----

Checkout all untracked files::

 git clean [options]

Options:

-n  shows what to get deleted

-d  remove directories

-f  delete them


Merge conflicts
=======

.. glossary::
	git merge --abort
		Aborting a merge in case a conflict appears
	
	git checkout --ours file-to-checkout
	git checkout --theirs file-to-checkout
		Choosing either side of a merge conflict

Example of file with merge conflict in an example file index.html:

.. parsed-literal::

	<<<<<<< HEAD:index.html
	everything here is my part (above the ====)
	`=======`
	everything here (below the ====)is from the iss53 branch
	>>>>>>> iss53:index.html

Can be edited manually, or using git mergetool

Aborting merge
--------------

Aborting a merge in case a conflict appears::

 git merge --abort

Choosing sides
--------------

Choosing either side of a merge conflict::

 git checkout --ours file-to-checkout
 git checkout --theirs file-to-checkout

get better comparison of merge conflict::

 git checkout --conflict=diff3 index.html

(can be set permanently: git config --global merge.conflictstyle diff3 (default conflictstyle is 'merge'))


Stashing
=======
.. glossary::
	git stash list
		lists all stashes
		
	git stash save "message here"
		add message to stash to remember what you did

stash
-----
https://git-scm.com/docs/git-stash 
to include untracked files into stash, add them to index first with git add

lists all stashes::

 git stash list 

add message to stash to remember what you did::

 git stash save "message here" 
 
get most recent stash::

 git stash pop
 
show diff of files in specific stash (or most recent if no stash specified)::

 git stash show -p stash@{1}
 
