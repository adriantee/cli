# DAILY commands

# linux commands

AMI Linux:

		ssh -i /Users/adrian.tee/Desktop/username.pem ec2-user@hostname

CentOS:

		ssh -i /Users/adrian.tee/Desktop/username.pem root@hostname

copy files/folders

		cp -a from/. to/

zip file (all files in folder)

		zip -r folder.zip destination_folder

unzip file

		unzip file.zip -d destination_folder

Change Ownership Of Directories:
		
		sudo chown -R apache:apache /var/www/html

Change Ownership Of File:
		
		sudo chown apache:apache filename

Create Key For Apache User:
		
		sudo -u apache ssh-keygen -t rsa

Set Correct Permission:
		
		chmod 700 ~/.ssh
		chmod 600 ~/.ssh/authorized_keys 

Create symlink:
		
		ln -s origin newdestination


More: <http://www.cyberciti.biz/faq/linux-remove-user-command/>


Generate Keys For Apache User:
		
		sudo -u apache ssh-keygen -t rsa

List all users:

		cat /etc/passwd

Delete user:

		userdel USERNAME

Find what files/dir are owned by user:
		find / -user USERNAME -print

Restrict User To Home Directory (chroot):

<https://bensmann.no/restrict-sftp-users-to-home-folder/>

		cat id_rsa.pub >> ~/.ssh/authorized_keys



# git commands

Add new git repo

	git add 
	git remote add origin git@bitbucket.org:REPONAME/REPO.git
	git pull origin develop

Check Current Branch:

		git branch

Switch Branch:

		git checkout develop

Checkout repo:

		git clone git@bitbucket.org:TEAMNAME/REPONAME.git FOLDER
		git checkout BRANCH

Stash local changes:

		git add *
		git stash

Get new branch

		git checkout --track origin/BRANCH

Reset local changes

		git reset --hard

Update branch

		git pull --rebase origin BRANCH

Update current branch 

		git pull origin BRANCH

Set without being in the directory:

		git --git-dir=/var/www/html/FOLDER/.git --work-tree=/var/www/html/FOLDER/ pull origin BRANCH 
		git --git-dir=/var/www/html/FOLDER/.git fetch
		git --git-dir=/var/www/html/FOLDER/.git --work-tree=/var/www/html/FOLDER merge origin/BRANCH

ssh-add ~/.ssh/id_rsa; ssh -vT git@github.com #-> success!


Find out sql version:

		mysql --version

