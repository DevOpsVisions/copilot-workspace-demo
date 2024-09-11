# Automating LAMP Stack Environment Setup

This guide provides detailed, step-by-step instructions for automating the setup of a LAMP stack environment using Terraform, a shell script, and GitHub Actions workflow.

## 1. Terraform Configuration

### Create and Configure Terraform Files

1. **Create a new directory for Terraform files:**

    ```bash
    mkdir terraform-lamp-setup
    cd terraform-lamp-setup
    ```

2. **Create a `main.tf` file:**

    ```hcl
    provider "azurerm" {
      features {}
    }

    resource "azurerm_resource_group" "rg" {
      name     = "rg-lamp-demo-uksouth-001"
      location = "uksouth"
    }

    resource "azurerm_virtual_network" "vnet" {
      name                = "vnet-lamp-demo-uksouth-001"
      address_space       = ["10.0.0.0/16"]
      location            = azurerm_resource_group.rg.location
      resource_group_name = azurerm_resource_group.rg.name
    }

    resource "azurerm_subnet" "subnet" {
      name                 = "subnet-lamp-demo-uksouth-001"
      resource_group_name  = azurerm_resource_group.rg.name
      virtual_network_name = azurerm_virtual_network.vnet.name
      address_prefixes     = ["10.0.1.0/24"]
    }

    resource "azurerm_public_ip" "pip" {
      name                = "pip-lamp-demo-uksouth-001"
      location            = azurerm_resource_group.rg.location
      resource_group_name = azurerm_resource_group.rg.name
      allocation_method   = "Static"
    }

    resource "azurerm_network_interface" "nic" {
      name                = "nic-lamp-demo-uksouth-001"
      location            = azurerm_resource_group.rg.location
      resource_group_name = azurerm_resource_group.rg.name

      ip_configuration {
        name                          = "ipconfig1"
        subnet_id                     = azurerm_subnet.subnet.id
        private_ip_address_allocation = "Dynamic"
        public_ip_address_id          = azurerm_public_ip.pip.id
      }
    }

    resource "azurerm_network_security_group" "nsg" {
      name                = "nsg-lamp-demo-uksouth-001"
      location            = azurerm_resource_group.rg.location
      resource_group_name = azurerm_resource_group.rg.name

      security_rule {
        name                       = "SSH"
        priority                   = 1001
        direction                  = "Inbound"
        access                     = "Allow"
        protocol                   = "Tcp"
        source_port_range          = "*"
        destination_port_range     = "22"
        source_address_prefix      = "*"
        destination_address_prefix = "*"
      }

      security_rule {
        name                       = "RDP"
        priority                   = 1002
        direction                  = "Inbound"
        access                     = "Allow"
        protocol                   = "Tcp"
        source_port_range          = "*"
        destination_port_range     = "3389"
        source_address_prefix      = "*"
        destination_address_prefix = "*"
      }

      security_rule {
        name                       = "HTTP"
        priority                   = 1003
        direction                  = "Inbound"
        access                     = "Allow"
        protocol                   = "Tcp"
        source_port_range          = "*"
        destination_port_range     = "80"
        source_address_prefix      = "*"
        destination_address_prefix = "*"
      }
    }

    resource "azurerm_network_interface_security_group_association" "nsg_association" {
      network_interface_id      = azurerm_network_interface.nic.id
      network_security_group_id = azurerm_network_security_group.nsg.id
    }

    resource "azurerm_virtual_machine" "vm" {
      name                  = "vm-lamp-demo-uksouth-001"
      location              = azurerm_resource_group.rg.location
      resource_group_name   = azurerm_resource_group.rg.name
      network_interface_ids = [azurerm_network_interface.nic.id]
      vm_size               = "Standard_DS1_v2"

      storage_os_disk {
        name              = "osdisk"
        caching           = "ReadWrite"
        create_option     = "FromImage"
        managed_disk_type = "Standard_LRS"
      }

      storage_image_reference {
        publisher = "Canonical"
        offer     = "UbuntuServer"
        sku       = "18.04-LTS"
        version   = "latest"
      }

      os_profile {
        computer_name  = "vm-lamp-demo-uksouth-001"
        admin_username = "azureuser"
        admin_password = "Password1234!"
      }

      os_profile_linux_config {
        disable_password_authentication = false
      }

      provisioner "remote-exec" {
        connection {
          type        = "ssh"
          user        = "azureuser"
          password    = "Password1234!"
          host        = azurerm_public_ip.pip.ip_address
        }

        script = "install-lamp.sh"
      }
    }
    ```

3. **Initialize and apply the Terraform configuration:**

    ```bash
    terraform init
    terraform apply -auto-approve
    ```

## 2. Shell Script

### Purpose and Usage of the Shell Script

The shell script `install-lamp.sh` automates the installation of the LAMP stack on the VM.

1. **Create the `install-lamp.sh` script:**

    ```bash
    #!/bin/bash

    # Update and upgrade the system
    sudo apt update && sudo apt upgrade -y

    # Install LAMP
    sudo apt install lamp-server^ -y

    # Verify Apache installation
    apache2 -v

    # Verify MySQL installation
    mysql -V

    # Verify PHP installation
    php -v
    ```

2. **Make the script executable:**

    ```bash
    chmod +x install-lamp.sh
    ```

## 3. GitHub Actions Workflow

### Using GitHub Actions to Automate the Provisioning Process

1. **Create a GitHub Actions workflow file `.github/workflows/terraform.yml`:**

    ```yaml
    name: Terraform Azure Deployment

    on: workflow_dispatch

    jobs:
      terraform:
        name: 'Terraform'
        runs-on: ubuntu-latest

        steps:
          - name: 'Checkout GitHub Action'
            uses: actions/checkout@v2

          - name: 'Set up Terraform'
            uses: hashicorp/setup-terraform@v1
            with:
              terraform_version: 1.0.0

          - name: Authenticate with Azure
            uses: azure/login@v1
            with:
              creds: ${{ secrets.AZURE_CREDENTIALS }}

          - name: 'Terraform Init'
            run: terraform init
            working-directory: ./terraform-lamp-setup

          - name: 'Terraform Apply'
            run: terraform apply -auto-approve
            working-directory: ./terraform-lamp-setup
            env:
              ARM_CLIENT_ID: ${{ secrets.ARM_CLIENT_ID }}
              ARM_CLIENT_SECRET: ${{ secrets.ARM_CLIENT_SECRET }}
              ARM_SUBSCRIPTION_ID: ${{ secrets.ARM_SUBSCRIPTION_ID }}
              ARM_TENANT_ID: ${{ secrets.ARM_TENANT_ID }}
    ```

2. **Add the necessary secrets to your GitHub repository:**

    - `AZURE_CREDENTIALS`
    - `ARM_CLIENT_ID`
    - `ARM_CLIENT_SECRET`
    - `ARM_SUBSCRIPTION_ID`
    - `ARM_TENANT_ID`

By following these steps, you will automate the setup of a LAMP stack environment using Terraform, a shell script, and GitHub Actions workflow.
