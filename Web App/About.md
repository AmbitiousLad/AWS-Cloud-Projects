🚀 Deploying a WordPress Website in the Cloud: A Step-by-Step Guide

![Screenshot 2024-08-20 191722](https://github.com/user-attachments/assets/b9635e17-25cd-4b59-890f-3ff92a74b146)


Excited to share a recent project where I deployed a WordPress website using cloud technologies to ensure scalability and reliability. Here's a quick overview of the process:

1.Provisioning an EC2 Instance:

Set up an Amazon EC2 instance with a suitable configuration (e.g., t2.micro for small projects) to serve as the virtual server for the WordPress installation.
Installing Apache:

•First we created an virtual machine (ec2) instance with operating system as Ubuntu , with instance type t2.micro.


![Screenshot 2024-08-20 191201](https://github.com/user-attachments/assets/5845d107-aa23-429b-84f4-0f8693611561)

• Then we have to allow all http and https requests to the machine in order to attend the web requests and responds to it.

![Screenshot 2024-08-20 191242](https://github.com/user-attachments/assets/71d7cbc9-cd0b-4e4b-8185-e37b373b047a)

• Then the instance is created finally.


![Screenshot 2024-08-20 211148](https://github.com/user-attachments/assets/09e0540b-2c2b-4037-9850-a7e11da86cd9)


2.Installed Apache HTTP Server on the EC2 instance to handle HTTP requests and serve web pages. Apache is known for its performance and flexibility in hosting web applications.
Configuring SQL Server:

• Connected to the EC2 Instance: We first used an SSH client to connect to our EC2 instance, allowing us to control it via the command prompt on Linux/Ubuntu.

![Screenshot 2024-08-20 195707](https://github.com/user-attachments/assets/ac91a211-f561-419c-86a3-b4c4a1c394c7)

• Installed Apache Server: We installed Apache on the machine to act as an intermediary between WordPress and the client.
![Screenshot 2024-08-20 195740](https://github.com/user-attachments/assets/78a55304-e78f-48f4-977f-0482d79ef427)

• Then Apache server is finally installed.

![Screenshot 2024-08-20 195613](https://github.com/user-attachments/assets/e8215d2e-665c-4243-a317-36ce71f0b446)



3.Set up SQL Server (or an alternative like MySQL) for database management. This involves creating a database and configuring access permissions for WordPress to store and retrieve content.
Deploying WordPress:

• The command sudo apt install mysql-server is used to install MySQL Server on a Linux-based operating system, such as Ubuntu or Debian.

![Screenshot 2024-08-20 224043](https://github.com/user-attachments/assets/740e6c7e-0d55-46e5-b1c2-4171c654f600)

• sudo mysql -u root:

Action: Logs into the MySQL command-line client as the root user.
Purpose: Allows you to execute MySQL commands with administrative privileges.


• ALTER USER 'root'@localhost IDENTIFIED WITH mysql_native_password BY 'Demopassword@123';:

Action: Alters the authentication method for the MySQL root user and sets a new password.
Purpose:
ALTER USER: Modifies the properties of an existing MySQL user.
'root'@localhost: Specifies the user (root) and the host from which the user connects (localhost).
IDENTIFIED WITH mysql_native_password: Sets the authentication plugin to mysql_native_password, which is a commonly used authentication method.
BY 'Demopassword@123': Sets the password for the root user to Demopassword@123.
Reason: Changes the default authentication plugin and sets a strong password for security purposes.


•CREATE USER 'wp_user'@localhost IDENTIFIED BY 'Demopassword@123';:

Action: Creates a new MySQL user named wp_user with the specified password.
Purpose:
CREATE USER: Creates a new MySQL user account.
'wp_user'@localhost: Specifies the new user (wp_user) and the host from which the user connects (localhost).
IDENTIFIED BY 'Demopassword@123': Sets the password for the new user.
Reason: Creates a dedicated user account for WordPress to interact with the MySQL database, which helps in managing permissions and securing the database.


• CREATE DATABASE wp;:

Action: Creates a new database named wp.
Purpose:
CREATE DATABASE: Creates a new database in MySQL.
wp: The name of the new database.
Reason: Establishes a database for storing WordPress content, settings, and other data.


•GRANT ALL PRIVILEGES ON wp.* TO 'wp_user'@localhost;:

Action: Grants all privileges on the wp database to the wp_user user.
Purpose:
GRANT ALL PRIVILEGES: Grants full access to the specified database.
ON wp.*: Specifies that the privileges apply to all tables in the wp database.
TO 'wp_user'@localhost: Specifies the user and host to whom the privileges are granted.
Reason: Allows the wp_user account to perform all operations on the wp database, which is necessary for WordPress to manage its data.

![Screenshot 2024-08-20 203405](https://github.com/user-attachments/assets/567a769c-b436-4de8-89c5-4477efcede6d)

4.Installing WordPress and connecting to apache and deployed finally

• cd /tmp:

Action: Changes the current directory to /tmp.
Purpose: Navigates to the /tmp directory, which is commonly used for temporary files.

•wget https://wordpress.org/latest.tar.gz:

Action: Downloads the latest version of WordPress in a compressed .tar.gz archive from the specified URL.
Purpose: Fetches the WordPress installation package from the official WordPress site.

•Output of wget command:

Status: Shows that the download was successful.
Details: The file latest.tar.gz is 23.5 MB in size and was saved in the /tmp directory.

•ls:

Action: Lists the contents of the /tmp directory.
Purpose: Verifies that the file latest.tar.gz has been downloaded successfully.
Output: Displays the latest.tar.gz file among other files and directories in /tmp.


Downloaded and installed WordPress on the EC2 instance. Configured it to connect to the SQL Server database, and customized the installation for optimal performance.
Security and Optimization:

![Screenshot 2024-08-20 225136](https://github.com/user-attachments/assets/8b88c6de-05e9-46f6-9d8d-7b96bedf5cab)


Thoroughly tested the deployment to ensure everything was running smoothly. Once verified, the website was launched, ready to handle visitors from around the globe.
Deploying WordPress on the cloud with these technologies not only ensures high availability and scalability but also provides a robust platform for managing dynamic content efficiently. 🌐✨

If you're interested in learning more about this process or need help with your own cloud deployment, feel free to reach out!

#WordPress #CloudComputing #AWS #Apache #SQLServer #EC2 #WebDevelopment #TechDeployment #CloudArchitecture
