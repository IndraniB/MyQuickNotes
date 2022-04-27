# Install Mysql on Linux ubuntu

# Table of Contents
1. [What is this document](#purpose)
1. [Steps](#steps)

---
## What is this document <a name="purpose"></a>
.
## Reference link:
https://phoenixnap.com/kb/install-mysql-ubuntu-20-04

## Steps:
1. Login to the server from terminal
1. sudo apt install mysql-server
1. sudo mysql_secure_installation
1. sudo systemctl enable --now mysql.service
1. systemctl status mysql.service
1. sudo ufw status 
1. sudo  ufw allow mysql

## Create new user in mysql
https://www.digitalocean.com/community/tutorials/how-to-create-a-new-user-and-grant-permissions-in-mysql
- CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
    - CREATE USER admin@10.162.255.140 IDENTIFIED BY 'User@12345’;


## Grant privilege
- GRANT ALL PRIVILEGES ON tenant_iam TO user@10.162.255.140;
- GRANT ALL PRIVILEGES ON * . * TO ‘root’@‘localhost';
    - GRANT ALL PRIVILEGES ON * . * TO ‘admin@’10.162.255.140';
- FLUSH PRIVILEGES;

## Change root password 
mysql is the default database in mysql server instalation. This database saved all user information. We need to loging to this database and change password for any user

- mysql -u root
- use mysql;
- update user set password=PASSWORD("root") where User='root';
- flush privileges;
- quit

## Start and stop mysql server
- sudo /etc/init.d/mysql stop
- sudo /etc/init.d/mysql start
- sudo service mysql restart

## Drop mysql users
- DROP USER 'admin'@'localhost';

## Skip all grants
- restart mysqld --skip-grant-tables option

## Troubleshotting
### After creating an user, you want to connect to database using the credential. If you are getting error in Workbench but you are able to log in from terminal then follow this steps: 

```
First simply log in with your current password:
sudo mysql -u root -p
Then change your password because having low strength password gives error sometimes.
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new-strong-password';

FLUSH PRIVILEGES;
Then simply exit and again login with your new password:
quit

sudo mysql -u root -p
Once you successfully logged in type the command:
use mysql;
It should show a message like 'Database changed' then type:
UPDATE user SET plugin='mysql_native_password' WHERE User='root';
After that type:
UPDATE mysql.user set authentication_string=PASSWORD('new-strong-password') where user='root';
Then type:
FLUSH PRIVILEGES;
Then simply exit:
quit
Now try to log in with your new password in your WORKBENCH. Hope it will work. Thank you.

```

### Not able to ssh into the server, got below message

- Error
    ``` 
    Indranis-MacBook-Pro:.ssh indranibandyopadhyay$ ssh root@10.162.255.140
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    @    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
    Someone could be eavesdropping on you right now (man-in-the-middle attack)!
    It is also possible that a host key has just been changed.
    The fingerprint for the ECDSA key sent by the remote host is
    SHA256:8PETxh5l01eZOIOFgMTSrbYvI4tLS0f5nJEn0TXL9Q8.
    Please contact your system administrator.
    Add correct host key in /Users/indranibandyopadhyay/.ssh/known_hosts to get rid of this message.
    Offending ECDSA key in /Users/indranibandyopadhyay/.ssh/known_hosts:9
    ECDSA host key for 10.162.255.140 has changed and you have requested strict checking.
    Host key verification failed.

    ```

- Solution
    - Read solution here: https://stackoverflow.com/questions/20840012/ssh-remote-host-identification-has-changed
    
    ```
    Here is the simplest solution

    ssh-keygen -R <host>
    For example,

    ssh-keygen -R 192.168.3.10
    From ssh-keygen man page:

    -R hostname Removes all keys belonging to hostname from a known_hosts file. This option is useful to delete hashed hosts (see the -H option above).
    ```

