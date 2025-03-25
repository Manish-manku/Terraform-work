# Terraform Guide

## Introduction to Terraform

Terraform is a tool that helps automate cloud infrastructure. With Terraform, you can create and manage cloud resources like virtual machines, storage, and networking across providers like AWS, Azure, and Google Cloud.

## Installing Terraform on Linux

### 1. Update Your System
Before installing anything, update your system:
```sh
sudo apt update && sudo apt upgrade -y
```
![image alt](https://private-user-images.githubusercontent.com/119393298/425764883-b9d99020-b516-4adc-9ca8-c6623d5e1edc.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY0ODgzLWI5ZDk5MDIwLWI1MTYtNGFkYy05Y2E4LWM2NjIzZDVlMWVkYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT00MTIzN2MyNzZjY2Y5YzNhZjE4YjVjODFiNWVkYjhmZTA1YzIxYmRjZGFhODAyZmJhMmFiMDk3YzNlYmU3YjAyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.xnlT3QSYuwl3GnF8D4hqc2RITDZodDcuPBV7PmvFAI8)
### 2. Install Required Dependencies
Run the following command to install necessary packages:
```sh
sudo apt install -y gnupg software-properties-common curl
```
![image alt](https://private-user-images.githubusercontent.com/119393298/425764914-facd499e-105e-4e07-aa1e-a8d9400845ce.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY0OTE0LWZhY2Q0OTllLTEwNWUtNGUwNy1hYTFlLWE4ZDk0MDA4NDVjZS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02MGExZWQwMzBkMDFlZGVmMWVjMGEzNTdjMTk2YTQzMmRhMzA3MmEzNzczZmRmMzBhNmU2ZDc4MTI5YjBlMzU1JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.UKF8EmC1Jr7b72RlIVZVJNd_fUnfamfuW2eKmenmTrA)
### 3. Add HashiCorp’s GPG Key
```sh
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```
![image alt](https://private-user-images.githubusercontent.com/119393298/425764940-b7e41f16-8b0a-41d9-8dbb-dc963a21fe6f.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY0OTQwLWI3ZTQxZjE2LThiMGEtNDFkOS04ZGJiLWRjOTYzYTIxZmU2Zi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT00OGRkZjllMWJhNDgxMTQ4NmE4MDRlNDk0MWQ0YTBlNzljODI1MmZlNjRkYzkzNTg3NGNmYzRjMDBiOWE4MWE5JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.cgLFejIqjIw3_atdeor1zsquTq_IFYctfKz3hbfe6sI)
### 4. Add the Terraform Repository
```sh
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```
![image alt](https://private-user-images.githubusercontent.com/119393298/425764981-93a1e4fa-dee8-483d-96d1-b67fd0939e85.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY0OTgxLTkzYTFlNGZhLWRlZTgtNDgzZC05NmQxLWI2N2ZkMDkzOWU4NS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1mZTJhNGIwODQzMmNmYWRkZjhlN2YzYTY1ZGZhMGYyZDFmZDBiYzU0NzU5YWMwOTk5NDEwYmM5MzBhODgwODEzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.87mVUgrD8vn2aeQmqBLbudOa3axdb6pWMVscfPNBCcs)
### 5. Install Terraform
```sh
sudo apt update
sudo apt install terraform -y
```
>>> Verify Installation
Run the following command to check if Terraform is installed:
```sh
terraform -version
```
![image alt](https://private-user-images.githubusercontent.com/119393298/425765010-ddac5ae5-0fb1-4404-919c-d4d8424693d4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY1MDEwLWRkYWM1YWU1LTBmYjEtNDQwNC05MTljLWQ0ZDg0MjQ2OTNkNC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03YmMyNzNjZTU0NDcyMjU1MDg4ZWY5NDkxOWIwNjhhODFjYzI5NDgxMTA3OGQ2MGE3MjU5NWNjZDJhMjM2YzNkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.jey8wNHyyJ7EwE85VRAimpFAUrG-cqRtBoJQAxTc1lI)
## Setting Up AWS for Terraform

### 1. Install AWS CLI
```sh
sudo snap install aws-cli --classic
```
![image alt](https://private-user-images.githubusercontent.com/119393298/425765034-42525147-97d8-4586-823f-ea6b75783205.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY1MDM0LTQyNTI1MTQ3LTk3ZDgtNDU4Ni04MjNmLWVhNmI3NTc4MzIwNS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1iYmVlNzZlMWExODhhNzU4ZGFhYmYwM2NiZDBiNGE4ZDQ3MTEwNzEwOGQ2ZGEwMGQ4ZTVmZmM2NGE5NGRkYTgxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.LUF2l0fibjkKwazgLEZPJoLl0SrqLpdcxcEoNmUpEt8)
### 2. Configure AWS Credentials
Run the command:
```sh
aws configure
```
Enter your AWS Access Key, Secret Key, and Region.
![image alt](https://private-user-images.githubusercontent.com/119393298/425765135-39325b89-43f9-4feb-929c-9ad02f6555c3.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY1MTM1LTM5MzI1Yjg5LTQzZjktNGZlYi05MjljLTlhZDAyZjY1NTVjMy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03YjIwMTU1MmY4YjEwOTVkMDc0NDRlOTU5NWZjZGZlZDY4YWY5OTBmYjg0Y2M1ZWM2Y2Q5ZTc1YjIwNWYxNGI2JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.fIJoQ-BaGRjmxyI2eLhC9mj4j_XjVAjX3vQYA4dNofI)
Alternatively, you can manually set credentials:
```sh
aws_access_key_id = YOUR_ACCESS_KEY
aws_secret_access_key = YOUR_SECRET_KEY
region = us-east-1
```

## Writing Terraform Configuration to Launch an EC2 Instance

### 1. Create a Project Directory
```sh
mkdir terraform-ec2 && cd terraform-ec2
```
![image alt](https://private-user-images.githubusercontent.com/119393298/425765165-50d5ae46-f690-40f1-88ad-083d84a6e1d5.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY1MTY1LTUwZDVhZTQ2LWY2OTAtNDBmMS04OGFkLTA4M2Q4NGE2ZTFkNS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1kMGQxMTM1YjUxNzhhNjk5NmEyYWE2MTAyMDlmMmNlY2VjMzBlNDE5MjBjZGI0YWQ2MDVlMTE4NTllZDljYWZlJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.u5NsCHfg102iFpon1xdgk6siEh7SqqNaCyqo13xIo4Y)

### 2. Create a Terraform File
Create a file named `main.tf` and add the following configuration:

```hcl
provider "aws" {
    profile = "default"
    region  = "ap-south-1"
}

resource "aws_instance" "my_server" {
    ami           = "ami-0cbf43fd299e3a464"
    instance_type = "t2.micro"

    tags = {
        Name = "MyTerraformInstance"
    }
}
```
Save the file and run the following commands:
### 3. Initialize Terraform
```sh
terraform init
```
![image alt](https://private-user-images.githubusercontent.com/119393298/425765257-5907cf48-0f45-4071-b942-e7405edbfa69.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY1MjU3LTU5MDdjZjQ4LTBmNDUtNDA3MS1iOTQyLWU3NDA1ZWRiZmE2OS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1jMDFlODYwNWMzNjEzYjk4MWFhNWZjNGFiY2Q4NTg2NTMyMTVlM2QxMTUwMGM3OTJmMjUwOWJmNzhhZjFkOWIyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.8shQNwytYrNRPq5RbiSbMN8B7BAv1eiF9es-AGAMH_M))
### 4. Plan the Deployment
```sh
terraform plan
```
![image alt](https://private-user-images.githubusercontent.com/119393298/425765307-1bb302e3-9c78-40fc-8f23-354101b64406.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY1MzA3LTFiYjMwMmUzLTljNzgtNDBmYy04ZjIzLTM1NDEwMWI2NDQwNi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1iNzM2ZTgwMjkxZjdkNGJlYTg5ZGQyNzk1OWQ0MDg3YzQ0YzVmMGFmNGZlMzA3NGFlYzRkZTk0MzBiNjE1ZGI4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.qDcfoViiKs15CfOLgnPUSoIwGfmhbRmJ1o1RZh2M8XA)
### 5. Deploy the Instance
```sh
terraform apply -auto-approve
```
Your EC2 instance should now be running in AWS!
![image alt](https://private-user-images.githubusercontent.com/119393298/425765460-8eae6744-ab7d-45a1-9ba8-42d96e823ac4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDI5MjUyMjksIm5iZiI6MTc0MjkyNDkyOSwicGF0aCI6Ii8xMTkzOTMyOTgvNDI1NzY1NDYwLThlYWU2NzQ0LWFiN2QtNDVhMS05YmE4LTQyZDk2ZTgyM2FjNC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzI1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMyNVQxNzQ4NDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hODRiZTdmY2M3ZWEyOWQyZGZmZDc5NDhjMmM2ZGNhYzk4OTE0OGQxMjNjMjNiMTEwZDI1ZWMzMTdjYTVkMmIyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.cS8lVkaQuKm2crMe6KXVx_e_5LMz9bkAZfso0g5OLBU)
