1.How to install github in ubunut?
	$ sudo apt-get install git

2.Global settings of github
	$ git config --global user.name "your githubname"
	$ git config --global user.email "email@example.com"

3.create local repository
	$ mkdir myrepository
	$ cd myrepository

	we can use command of "pwd" to check out the directory of repository's folder.

4.Using git init command to change directory into manager repository.

	$ git init
	Initialized empty Git repository in /Users/michael/learngit/.git/

	When we create a GIt repository it will create a new director called .git on local directory.
	This directory is used to manager the repository.
	**Do not delete or modify this dirctory(.git)**

5.Adding our first file to the repository.

	1.Create a file called test.txt.

	$ sudo vim test.txt

	the content of this file is:

	This is just a test file.


	2.Putting it to the git repository.
	$ sudo git add test.txt

	3.Adding it into the git repository.
	$ sudo git commit -m "Test file"
	[master (root-commit) eaadf4e] wrote a readme file
	 1 file changed, 2 insertions(+)
	 create mode 100644 test.txt

	-m means the introduction of this submitting.
	You can type any thing of it but you'd better type something is significant.

	You can also add multiple files as one time by using this command:
	$ sudo git add file1.txt
	$ sudo git add file2.txt file3.txt
	$ sudo git commit -m "add 3 files."

	How to delete the file from your repository?
	$ sudo git rm test.txt
	$ sudo git commit -m "remove test.txt"

	Deleting multiple files:
	$ sudo git rm test.txt test1.txt test2.txt
	$ sudo git commit -m "remove test.txt"

6.Adding to the remote repository
1.Creating a SSH key of github:
	$sudo ssh-keygen -t rsa -C "youremail@example.com"
	previous command will create two files calld: id_rsa id_rsa.pub
	Then we will copy these files to our local user directory's .ssh directory.
	afterward we login the github webside and open the "Account settings" find page "SSH and GPG keys"
	copy all the content in id_rsa.pub into SSH keys.
	Using next command to check the SSH is ok or not.
	$ sudo ssh -T git@github.com
	Hi haoxr! You've successfully authenticated, but GitHub does not provide shell access.
	Showing that message means it gose success.

2.login to the github webside and create a new repository
3.Creating a new repository the name is Myleaning.
4.Connecting the repository between local and distance
	***run this command in your local repository directory:***
	$ sudo git remote add origin git@github.com:Naruterador/Myleaning.git
	if we set the settings wrong,we can modify it in ./git/config.
5.Pushing the content of local repository to the remote repository.
	$ sudo git push -u origin master
	Counting objects: 20, done.
	Delta compression using up to 4 threads.
	Compressing objects: 100% (15/15), done.
	Writing objects: 100% (20/20), 1.64 KiB | 560.00 KiB/s, done.
	Total 20 (delta 5), reused 0 (delta 0)
	remote: Resolving deltas: 100% (5/5), done.
	To github.com:michaelliao/learngit.git
	 * [new branch]      master -> master
	Branch 'master' set up to track remote branch 'master' from 'origin'.
	
	afterward you just using next command to push your objects to the remote directory:
	$ sudo git push origin master
	
Error collection:
1.$ git push -u origin master
	git@github.comPermission denied (publickey)
		We need to check out two files id_rsa and id_rsa.pub if the files in the rights position(user directory)
		if not just copy the files to the right position.




	To git@github.com:yangchao0718/cocos2d.git
	! [rejected]        master -> master (non-fast-forward)
	error: failed to push some refs to 'git@github.com:yangchao0718/cocos2d.git
	hint: Updates were rejected because the tip of your current branch is behin
	hint: its remote counterpart. Integrate the remote changes (e.g.
	hint: 'git pull ...') before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.
		Using:
			$ git pull origin master //fetch and merge the code
			$ git push origin master //then push




2.Git Pull Failed
  fatal: refusing to merge unrelated histories.
  Using next command to force the pull.
  $ git pull origin master --allow-unrelated-histories
  Then push it.
  $ git push origin master

3.Git Pull Failed
  error: You have not concluded your merge (MERGE_HEAD exists).
  fatal: Exiting because of unfinished merge.
  You need commit the file first using git commit -m "commit info",afterward you can pull or merge the files
  Or you can just cover all the files:
  $ git reset --hardgit pull




The configuration for git config:
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = git@github.com:Naruterador/NA_SYSTEM.git
