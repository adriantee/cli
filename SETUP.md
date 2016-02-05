# SETUP new server on AWS

# Installation

The following will install php vx.x mysql x.x

AWS Linux AMI

1. Setup:

		sudo yum -y update
		sudo yum install httpd php mysql-server

2. Auto start httpd service:

		sudo chkconfig httpd on
		sudo chkconfig mysqld on
		sudo chkconfig --list|grep http

	Doublecheck if added: 
		
		sudo chkconfig
		
	You should see something like below:

		>>[root#] 0:off  1:off  2:on 3:on 4:on 5:on 6:off

3. Start services:

		sudo service httpd start
		sudo service mysqld start

4. Set permissions:

		sudo chown -R ec2-user /var/www/html
		sudo chmod -R 755 /var/www/html

5. Install phpMyAdmin:

		sudo yum --enablerepo=epel install phpmyadmin
		sudo ln -s /usr/share/phpMyAdmin /var/www/html/pma
		sudo yum install libmcrypt libmcrypt-devel php-mcrypt php-mbstring

		mysqladmin -u root password thisisalongpassword

6. Secure phpmyadmin

		cd /var/www/html/phpmyadmin/ rm -rf config

7. Make symlinks to new volume for /var/www/html



Create new partition for extra free space:
---------------------------------------------
1. fdisk /dev/hda 
2. type p (it will print partition table) 
3. type n (for creating a new pratition) 
4. press enter (it will take the default value) 
5. Press enter (it will take last cyclinder as default value) 
6. Press p (it will print the new partition table , can u see "/dev/hda8 
Linux") 
7. Press w (to save) 
8. mkfs -t ext3 /dev/hda8 ( make it as a ext3 filesystem) 
9. mkdir /test 
10. mount /dev/hda8 /test (to mount the partition) 

		
		mount /dev/xvdb1 /home

edit /etc/fstab to AUTO MOUNT:

		/dev/xvdb1              /home                   ext4    defaults        0 0


create symlinks for var/www to /home

		ln -s /home/www /var/www

-create symlink to PMA

		ln -s /home/www/html/pma /home/www/html/wp_cn/pma


Add mount to rc local to mount all every restart:
		
		/etc/rd.c/rc.local
		mount -a





Adding new public/private keys:
===============================
1. Generate private/public key pair

		ssh-keygen -t rsa

2. copy public key to /root/.ssh/authorized_keys file

3. convert private key to .pem

		openssl rsa -in ~/.ssh/id_rsa -outform pem > id_rsa.pem

4. change permisson for private key

		sudo chmod 600 id_rsa.pem


# Deployment

<https://gist.github.com/oodavid/1809044#file_deploy.php>

<https://gist.github.com/aronwoost/1105010#generate-key-for-apache-user>

<http://brandonsummers.name/blog/2012/02/10/using-bitbucket-for-automated-deployments/>

<http://jonathannicol.com/blog/2013/11/19/automated-git-deployments-from-bitbucket/>


1. Own the .git directory with the 'web' user who is usually apache, www-data, etc.

2. Generate key for that user

3. Do git fetch to add hostkey to known host.

4. Run script.









# FAQ

Make git command universal:
---------------------------

		alias git="/usr/local/cpanel/3rdparty/bin/git"



Linux folders
---------------

Http config

		/etc/httpd/conf/httpd.conf

Repo list:

		/etc/yum.repos.d


On Mac (change virtual directory):
		
		/etc/host






# Troubleshooting

Fix permissions:
---------------------------

		/home/USER must be 700 or 755






Repositories
------------

GET & ENABLE remi repo:

<https://www.mojowill.com/geek/howto-install-php-5-4-5-5-or-5-6-on-centos-6-and-centos-7/>

DO THIS FIRST:

		sudo rpm -Uvh http://mirror.webtatic.com/yum/el6/latest.rpm
		sudo yum install -y php55-mysqlnd php55 php55-xml php55-mcrypt php55-mbstring php55-cli mysql55 mysql55-server httpd24
		sudo yum install php55w php55w-opcache

<http://www.rackspace.com/knowledge_center/article/installing-mysql-server-on-centos>




Alternative commands:

		sudo yum -y update
		sudo yum install -y gcc make gcc-c++
		sudo yum install -y php55-mysqlnd php55 php55-xml php55-mcrypt php55-mbstring php55-cli mysql55 mysql55-server httpd24







# Cpanel

<https://www.buycpanel.com/cpanel_license/cpanel-vps-optimized>

<http://www.licensepal.com/products/cpanel.php>

Activate license:

		/usr/local/cpanel/cpkeyclt




Add new public IP, after assign new private ip and assign elastic IP :
=======================================================================

http://blog.ls20.com/get-two-public-ips-on-an-amazon-ec2-instance-for-free/

***** 1. add the new private IP /20 ----> sudo ip addr add dev eth0 192.168.xxx.xxx/24
sudo ip addr add dev eth0 172.31.8.244/20

iptables -L -n


# SSL






yum install mod24_ssl






Generate csr
Submit to CA
get 1 crt file

also configure ssl.conf to include the files
copy to httpd conf:


<VirtualHost *:443>
    ServerName www.website.com
    DocumentRoot /var/www/html/wp_id
    SSLEngine on
    SSLCertificateFile /etc/httpd/conf/ssl.crt/downloadedssl.crt
    SSLCertificateKeyFile /etc/httpd/conf/ssl.key/privatekey.pem
    <Directory /var/www/html/wp_id>
        AllowOverride All
    </Directory>
</VirtualHost>



check CN
openssl x509 -in server.crt -noout -subject


how to guide:
http://glynjackson.org/weblog/installing-ssl-aws-ec2/






# SSH

<http://wiki.centos.org/HowTos/Network/SecuringSSH>


copy key to root directory:

		scp -i /Users/adrian.tee/Desktop/PRIVATEKEY.pem /Users/adrian.tee/Desktop/PUBLICKEY.pub root@HOST:/root

append public key to host:

		remote> /root/.ssh
		local> scp .ssh/id_dsa.pub HOST:
		local> ssh HOST
		remote> cat id_dsa.pub >> .ssh/authorized_keys
		remote> rm id_dsa.pub
		remote> exit



Stop asking for passphrase:
		
		eval $(ssh-agent)
		ssh-add




# PhpMyAdmin

download

		wget xxxxx.tar.gz     >> get from https://www.phpmyadmin.net/downloads/

SET new password:

		mysqladmin -u root password NEWPASSWORD

CHANGE password:

		mysqladmin -u root -p'oldpassword' password newpass


# Misc

Set Execute Bit For Public Www Folder:

<http://serverfault.com/questions/124800/how-to-setup-linux-permissions-for-the-www-folder>

<http://askubuntu.com/questions/26848/permissions-issue-how-can-apache-access-files-in-my-home-directory>



Cant view web server on CentOS:

<http://stackoverflow.com/questions/10729247/apache-not-accepting-incoming-connections-from-outside-of-localhost>

state NEW tcp dpt:80
Which you can do like this:

sudo iptables -I INPUT 4 -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
(In this case I am choosing to add the new rule in the fourth line)

Remember that after editing the file you should save it like this:

sudo /etc/init.d/iptables save



Set IIS gzip and deflate

cd C:\Inetpub\AdminScripts\

cscript adsutil.vbs SET W3SVC/Filters/Compression/Deflate/HcFileExtensions "htm html txt css js"

cscript adsutil.vbs SET W3SVC/Filters/Compression/gzip/HcFileExtensions "htm html txt css js"

