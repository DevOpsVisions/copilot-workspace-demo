# Preparing a LAMP Stack Environment for Question2Answer or WordPress Hosting

This guide provides step-by-step instructions for setting up a testing environment on Azure using an Ubuntu virtual machine (VM) on Azure, installing essential software, and configuring the environment for hosting a Question2Answer (Q2A) or WordPress application. 

By following this guide, you will create a fully functional server environment, ready to deploy and manage your Q2A or WordPress site efficiently.

## 1. Create a Resource Group

Before deploying any Azure resources, you need a resource group. An Azure resource group is a logical container that holds related resources for an Azure solution.

Open Azure Cloud Shell and run the following command to create a resource group:

```powershell
az group create --name rg-q2a-demo-uksouth-001 --location uksouth
```
This command creates a resource group named rg-q2a-demo-uksouth-001 in the uksouth region.

## 2. Create a Virtual Machine (VM)

Next, you'll create an Ubuntu 22.04 VM that will serve as the server for your Q2A/WordPress installation.

```powershell
az vm create --resource-group rg-q2a-demo-uksouth-001 --name vm-q2a-demo-uksouth-001 --image Ubuntu2204 --admin-username azureuser  --admin-password 'password'
```

- VM Name: vm-q2a-demo-uksouth-001
- Image: Ubuntu2204
- Admin Username: azureuser
- Admin Password: YourPasswordHere

After the command executes, Azure will output the details of the VM, including the `publicIpAddress`. Make sure to note this, as it will be used for SSH access and web navigation.

## 3. Open Port 80 for HTTP Traffic

To allow web traffic to reach your Q2A application, you need to open port 80.

```powershell
az vm open-port --port 80 --resource-group rg-q2a-demo-uksouth-001 --name vm-q2a-demo-uksouth-001
```
This command enables HTTP traffic to your VM, allowing users to access the web server running on port 80.

## 4. Open Port 3389 for RDP (Optional)

If you plan to use Remote Desktop Protocol (RDP) to connect to your VM, you'll need to open port 3389.

```powershell
az vm open-port --port 3389 --priority 1100 --resource-group rg-q2a-demo-uksouth-001 --name vm-q2a-demo-uksouth-001
```

- **Priority: 1100** (Ensures it doesn’t conflict with other rules)

## 5. Connect to the VM via SSH

Now that your VM is up and running, connect to it using SSH.

```bash
ssh azureuser@yourPublicIpAddress
```
Replace yourPublicIpAddress with the public IP address of your VM, which was displayed after VM creation.

## 6. Update and Upgrade apt

It's essential to keep your system up to date. Begin by updating the package lists and upgrading installed packages.

```bash
sudo apt update
```

- `apt update:` Updates the list of available packages and their versions.

## 7. Install and Configure Xfce and XRDP (Optional)

If you require a GUI for your VM, you can install the Xfce desktop environment and XRDP for remote desktop access.

```bash
sudo DEBIAN_FRONTEND=noninteractive apt-get -y install xfce4
```
```bash
sudo apt install xfce4-session -y
```
```bash
sudo apt-get -y install xrdp
```
```bash
sudo systemctl enable xrdp
```
```bash
sudo adduser xrdp ssl-cert
```
```bash
echo xfce4-session >~/.xsession
```
```bash
sudo service xrdp restart
```

These commands set up a lightweight desktop environment (Xfce) and enable XRDP for RDP access. This is useful if you need to manage the VM through a graphical interface.

## 8. Install Google Chrome or Firefox

For browsing or downloading files directly on the VM, install a web browser like Google Chrome or Firefox.

**To Install Google Chrome:**

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
```bash
sudo dpkg -i google-chrome-stable_current_amd64.deb
```
```bash
sudo apt --fix-broken install -y
```

**To Install Firefox:**

```bash
sudo apt install firefox -y
```

## 9. Install Unzip or Unrar 

Install `unzip` or `unar` to extract the downloaded files.

**To Install Unzip**

```bash
sudo apt install unzip
```

**To Install Unrar**

```bash
sudo apt install unar
```

## 10. Install the LAMP Stack

The LAMP stack (Linux, Apache, MySQL, PHP) is required for hosting Q2A/WordPress site.

```bash
sudo apt update && sudo apt install lamp-server^ -y
```

## 11. Verify Installation

After installing the LAMP stack, verify that each component is correctly installed.

```bash
apache2 -v
mysql -V
php -v
```
These commands check the versions of Apache, MySQL, and PHP to ensure they're installed correctly.

## 12. Create a PHP Info File (Optional)

To verify PHP is functioning properly, create a PHP info page.

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```
Then, in your browser, navigate to http://yourPublicIpAddress/info.php to view the PHP configuration details.

## 13. Secure MySQL Installation

Secure your MySQL installation by running the MySQL secure installation script.

```bash
sudo mysql_secure_installation
```
This script prompts you to set a root password, remove anonymous users, disallow root login remotely, and more, to enhance your MySQL security.

## 14. Configure MySQL Root User

Finally, update the MySQL root user to use a native password authentication method and set a strong password.

```bash
sudo mysql
```

```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'YourSecurePassword';
```

```bash
exit
```

Replace `YourSecurePassword` with a strong password of your choice. This step is crucial for securing your MySQL database.

Following these steps will set up an environment for deploying your Question2Answer or WordPress site on Azure. Be sure to adjust the commands and configurations to meet your specific requirements.

## Reference

For automating the setup of a LAMP stack environment, refer to the [Automating LAMP Stack Environment Setup](automate-lamp-stack-setup.md) guide.
