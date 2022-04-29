# Simple Web Application

This is a simple web application using [Python Flask](http://flask.pocoo.org/) and [MySQL](https://www.mysql.com/) database. 
This is used in the demonstration of development of Ansible Playbooks.
  
  Below are the steps required to get this working on a base linux system.
  
  - Install all required dependencies
  - Install and Configure Database
  - Start Database Service
  - Install and Configure Web Server
  - Start Web Server

# A. Ubuntu
## 1. Install all required dependencies
  
  Python and its dependencies

    apt-get install -y python python-setuptools python-dev build-essential python-pip python-mysqldb

   
## 2. Install and Configure Database
    
 Install MySQL database
    
    apt-get install -y mysql-server mysql-client

## 3. Start Database Service
  - Start the database service
    
        service mysql start

  - Create database and database users
        
        # mysql -u <username> -p
        
        mysql> CREATE DATABASE employee_db;
        mysql> GRANT ALL ON *.* to db_user@'%' IDENTIFIED BY 'Passw0rd';
        mysql> USE employee_db;
        mysql> CREATE TABLE employees (name VARCHAR(20));
        
  - Insert some test data
        
        mysql> INSERT INTO employees VALUES ('JOHN');
    
## 4. Install and Configure Web Server

Install Python Flask dependency

    pip install flask
    pip install flask-mysql

- Copy app.py or download it from source repository
- Configure database credentials and parameters 

## 5. Start Web Server

Start web server

    FLASK_APP=app.py flask run --host=0.0.0.0
    
## 6. Test

Open a browser and go to URL

    http://<IP>:5000                            => Welcome
    http://<IP>:5000/how%20are%20you            => I am good, how about you?
    http://<IP>:5000/read%20from%20database     => JOHN

# B. RHEL - 8

## 1. Pre-requisites

    pip3 install flask
    pip3 install flask-mysql

## 2. Install and Configure Database

    ####wget https://repo.mysql.com/mysql80-community-release-el8-1.noarch.rpm
    ####yum localinstall mysql80-community-release-el8-1.noarch.rpm

    yum install mysql-server
    service mysqld start

Enter Database, configure 

        mysql> CREATE USER 'db_user'@'localhost' IDENTIFIED BY 'PasswOrd';
        mysql> GRANT ALL ON *.* to 'db_user'@'localhost'
        mysql> USE employee_db;
        mysql> CREATE TABLE employees (name VARCHAR(20));
        
  - Insert some test data
        
        mysql> INSERT INTO employees VALUES ('JOHN');
        
- Copy app.py or download it from source repository
- Configure database credentials and parameters 

## 3. Start Web Server

Start web server

    FLASK_APP=/opt/app.py nohup flask run &
    
## 4. Test

Open a browser and go to URL

    http://<IP>:5000                            => Welcome
    http://<IP>:5000/how%20are%20you            => I am good, how about you?
    http://<IP>:5000/read%20from%20database     => JOHN
