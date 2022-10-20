# Setting up Apache Server

How to setup a simple Apache server which could be used to serve your website. While this guide might show setup of Apache, it will consist of setting up other tools as well like mysql/phpmyadmin for Database.

Requirement : Linux Environment

&#x20;**Apache Server :**\
`sudo apt-get install apache2`

**Make sure to enable **_**mod\_rewrite**_** module of apache to be able to use pretty url :**

`sudo a2enmod rewrite`

**Install MySQL Server For Database :**\
`sudo apt-get install mysql-server`

Optional : We could use any language to connect to database and serve pages using  apache but for this lesson, we will be using php which is used in most CMS like WordPress and Drupal.

**Install PHP with helper packages :**\
`sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql`

Optional : We could use Command Line to Interact with Database, but another helpful GUI tool to interact with database is phpmyadmin.

**Install phpmyadmin :**\
`sudo apt-get install phpmyadmin apache2-utils`

To use phpmyadmin with apache we need include it into apache.conf\
`sudo nano /etc/apache2/apache2.conf`

Then add following line at the end of apahce2.conf file to include phpmyadmin :\
`Include /etc/phpmyadmin/apache.conf`

**Once done, make sure to restart the Apache Server :**\
`sudo systemctl restart apache2`

_Extra : In case you misconfigure phpmyadmin during installation you can use following command to reconfigure it :_\
`sudo dpkg-reconfigure phpmyadmin`

Extra: Might Need to Create user to able to access from Remotely as well  :\
`DROP USER 'root'@'localhost';`\
`CREATE USER 'root'@'%' IDENTIFIED BY '';`\
`GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;`\
`FLUSH PRIVILEGES;`

**CONFIGURE APACHE SERVER**

Next we need to configure apache to show where to send request from client. Following is the typical apache configuration in /etc/apache2/sites-available/default.conf for cms like WordPress.

```
<VirtualHost *:80>
ServerName yourdomain.com
ServerAlias www.yourdomain.com
DocumentRoot /location/path/of/your/website
<Directory /location/path/of/your/website>
Options Indexes FollowSymLinks MultiViews
AllowOverride All
Order allow,deny
allow from all
</Directory>
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
