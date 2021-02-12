Creating a Registration Page using Java,Mysql,tomcat,ubuntu,eclipse


## Installation:

### Java installation:
Download the latest java jdk version at the time of writing this document it is openjdk 14
1. `sudo apt-get install openjdk-14-jdk openjdk-14-jre`
2. test the installation with `javac -version`

### Tomcat installation:
Installing tomcat in windows/ubuntu
1. Download the zip file and extract it to ~/.tomcat
2. Thats it nothing more to do

### MySQL installation
install mysql in ubuntu by downloading the apt package
1. download the mysql deb `https://dev.mysql.com/downloads/repo/apt/`
2. install the deb package `sudo dpkg -i mysql-apt-config_w.x.y-z_all.deb`
3. update and install mysql server `sudo apt-get update && sudo apt-get install mysql-server && sudo apt-get install mysql-workbench-community`
4. verify the installation with `mysql --version`
5. run `mysql_secure_installation` then select appropriate options to install with good password that you will remember
6. This password is for root user of mysql,this is different from root user of ubuntu installation
7. As a best practice it is preferred to create a new user and database for this user,grant permission to this database.
8. `CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';` creates a new user
9. `GRANT all privileges ON database_name.* TO 'username'@'localhost';` grants all permissions to the user on specified database
10. to access an account of mysql use `mysql -u accountname -p`,to access root user of mysql `mysql -u root -p`,password(0000)
11. restart the mysql service with `sudo systemctl status mysql && sudo systemctl restart mysql && sudo systemctl status mysql`
12. then login to mysql account and work on some tables, do the same with mysql workbench software to verify the mysql connection


### Eclipse installation
Eclipse is an open source software editor for various languages(C,C++,Java(SE),Java(EE),Python,PHP).
1. Go to eclipse website and download the latest installer software,don't download the zip it will be standalone and needs a lot of setup manually to be configured.
2. After downloading the installer extract and run it in terminal `./eclipse-inst`
3. Install eclipse on home directory for easy access and privileges for users.
4. Take a shortcut on home screen and start menu 

#### Configuring Eclipse
1. To develop normal/core java projects use eclipse java ide.
2. to develop servlets/jsp/websites with java use eclipse java ee edition.
3. After installation change download the themes from eclipse market place,color themes,start autosave
4. in eclipse a project is used for even a single file,so it is a best practice to create a project then a main class file that is start of project then all other classes refer to this file.

#### Tomcat in eclipse
To make use of tomcat in eclipse java ee we click on servers option then select the same version of tomcat as the previous installed tomcat then locate the folder containing extracted tomcat code(~/.tomcat)
1. run the current jsp/servlet page in run as server and change the default browser to chrome browser for better debugging.


### creating a signup login page 
Using java,servlets,jsp,html,css,sql,tomcat,eclipse

Create a dynamic web project and create three jsp files 
login.jsp,register.jsp,welcome.jsp
1. create a basic html login,register,welcome pages then paste the code in jsp files
2. create appropriate java files to get data from jsp and database
3. install mysql connector java to tomcat library and in java build path of eclipse for easy access to mysql service
4. create a servlet that contains the account id,password,jdbc connection to mysql port and database name
5. Test this connection then complete the front end and backend with no errors.
6. create a table in mysql directly,use this table with matching column names in servlet code
7. `create table customer (customer char(20),password char(10),name char(20))`
8. Run the login jsp with tomcat then create a new user and save data,while loging in check the values with existing one
9. If same show the welcome page with custom page/custom feed.
