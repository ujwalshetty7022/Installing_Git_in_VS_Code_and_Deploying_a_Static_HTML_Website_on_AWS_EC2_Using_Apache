Installing Git in VS Code and Deploying a Static HTML Website on AWS EC2 Using Apache

Install Git on your local computer.
Go to the Git website and download Git for your operating system.
After installation, open VS Code.
Open the terminal inside VS Code by pressing Ctrl + ` (backtick).
Run the command git --version to confirm Git is installed successfully.

Create a new project in VS Code.
Create a new folder on your computer for your project.
Open that folder in VS Code.
Create your HTML, CSS, and JavaScript files inside it.
Save all your files.

Initialize Git in your project folder.
In the VS Code terminal, run:
git init
Add all files to the repository:
git add .
Commit the changes:
git commit -m "Initial commit"

Create a new repository on GitHub.
Go to GitHub and create a new repository.
Copy the HTTPS URL of the repository.

Connect your local project to GitHub.
In the VS Code terminal, run:
git remote add origin https://github.com/your-username/your-repo-name.git

Push your code to GitHub:
git branch -M main
git push -u origin main

Launch an EC2 instance in AWS.
Open AWS Management Console and go to EC2.
Launch a new instance using Ubuntu Server as the operating system.
Choose t2.micro as the instance type.
Create or use an existing key pair (.pem file).
In the security group, allow inbound rules for SSH (port 22) and HTTP (port 80).
Launch the instance and note the public IP address.

Connect to the EC2 instance from VS Code terminal.
In the terminal, run:
ssh -i "your-key.pem" ubuntu@your-ec2-public-ip

Install Apache web server on the EC2 instance.
Run the following commands one by one:
sudo apt update -y
sudo apt install apache2 -y
Start and enable Apache:
sudo systemctl start apache2
sudo systemctl enable apache2
Check if Apache is running:
sudo systemctl status apache2

Test Apache.
Open a browser and go to http://your-ec2-public-ip

You should see the default Apache page.

Install Git on the EC2 instance.
Run the following command:
sudo apt install git -y

Clone your GitHub project to the EC2 instance.
Change to the temporary directory:
cd /tmp
Clone the repository:
git clone https://github.com/your-username/your-repo-name.git

Deploy your project using Apache.
Remove the default Apache files:
sudo rm -rf /var/www/html/*
Copy your project files to the Apache directory:
sudo cp -r /tmp/your-repo-name/* /var/www/html/
Restart Apache:
sudo systemctl restart apache2

Allow web traffic.
Enable Apache through the firewall:
sudo ufw allow 'Apache Full'
sudo ufw enable
In AWS console, check the security group and ensure HTTP (port 80) is open to 0.0.0.0/0.

Access your website.
Go to your browser and open:
http://your-ec2-public-ip

Your HTML site should now appear live.

Update your website after making changes.
Whenever you change your HTML code in VS Code and push it to GitHub, update the EC2 instance by running:
cd /tmp/your-repo-name
git pull
sudo cp -r * /var/www/html/
sudo systemctl restart apache2

Summary:
Install Git on your local computer and use VS Code to build and push your HTML project to GitHub.
Launch an Ubuntu EC2 instance in AWS, install Apache, and clone your project from GitHub.
Copy your files to the Apache web directory and access your website using the EC2 public IP.
Whenever you make changes locally and push to GitHub, pull them on EC2 and restart Apache to reflect updates.
