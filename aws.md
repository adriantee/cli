SETUP NEW INSTANCE:
===================
sudo yum -y update
sudo yum install -y gcc make gcc-c++
sudo yum install -y php55-mysqlnd php55 php55-xml php55-mcrypt php55-mbstring php55-cli mysql55 mysql55-server httpd24

//sudo yum install php-mysql php php-xml php-mcrypt php-mbstring php-cli mysql httpd


SETUP AUTOSTART SERVICE:
========================
sudo chkconfig httpd on
sudo chkconfig mysqld on

sudo service httpd start
sudo service mysqld start



sudo chown apache:apache /var/www/html



# change permission to write for group (as ec2-user) 

sudo chgrp -R wheel /var/www/html
sudo chmod g+w /var/www/html


SET time zone to SQL:

[mysqld]
default_time_zone='+08:00'



INSTALL PMA:
============
http://sourceforge.net/projects/phpmyadmin/files/phpMyAdmin/

wget https://github.com/phpmyadmin/phpmyadmin/archive/STABLE.tar.gz

tar zxvf STABLE.tar.gz

mv phpMyAdmin-4.5.0.2-all-languages phpmyadmin

rm -rf phpMyAdmin-4.5.0.2-all-languages.tar.bz2



SHOW FREE SPACE DISK:
df -h


SHOW FREE MEMORY:
free -m

AWS setup[http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-LAMP.html]

CHANGE PERMISSION
==========================================
sudo chmod -R 755 /var/www/html

CHANGE OWNERSHIP
==========================================
sudo chown -R ec2-user /var/www/html


MAKE PRIVATE KEY NOT ACCESSIBLE TO OTHERS:
==========================================
sudo chmod 400 fuse-sg.pem