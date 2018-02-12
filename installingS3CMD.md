# S3cmd on SUSE Linux Setup Guide
			
## Install
- Boot up Virtual Machine
- If Azure VM, go to Azure portal and find the SUSE VM and “Start” it
- SSH (log into) into SUSE VM
  - Need IP and Username and Password (can be found and reset in Azure Portal page for respective VM)
  - Username and Password are case sensitive
  - Use Putty SSH tool for Windows, Terminal tool for Linux or OSX
  - Verify logged in correctly when you see the command prompt
Create and navigate to temporary install directory
- mkdir /var/tmp/s3
- cd /var/tmp/s3
Install
- Download S3cmd compressed file to /var/tmp folder
  - wget http://ufpr.dl.sourceforge.net/project/s3tools/s3cmd/1.6.1/s3cmd-1.6.1.tar.gz
- xtract S3cmd compressed file
  - tar -xf s3cmd-1.6.1.tar.gz
- Navigate to S3cmd Install folder
  -cd s3cmd-1.6.1
- Run installation file
  - sudo python setup.py install
  - Enter root (sudo) password when prompted 
- After install is finished, remove installation files
  - cd /var/tmp
  - sudo rm s3 -rf
 
## Configure
s3cmd --configure
Type in Access Key of AWS account when prompted
- Created when setting up AWS account, need admin to provide
Type in Secret Access Key of AWS account when prompted
- Created when setting up AWS account, need admin to provide
Press [Enter] key when prompted for default region
Create encryption password
- *Text not hidden*
Press [Enter] key when prompted for path to GPG program 
Press [Enter] key when prompted to use HTTPS protocol
Press [Enter] key when prompted for HTTP proxy path
Type in “Y” when prompted to test setup
Confirm that test worked
- If not, troubleshoot by making sure AWS account access set up properly and the Access keys are correct and type in “N” and then type in “n”
- If yes, type in “y” to finish configuration

## Usage
- To list all objects or buckets
  - s3cmd ls
- To list all objects inside of buckets
  - s3cmd la
- To download an object from bucket to local VM Hard Drive
  - Navigate over to directory you want to save file (through cd)
  - i.e cd /home
  - s3cmd get s3://bucket_name//object_name
  - Or just s3cmd get s3://bucket_name/ for whole bucket

## Command List for S3cmd
•	https://linux.die.net/man/1/s3cmd

## Easy copy and paste notation of above commands (copy here and just right click into Putty / Terminal to paste)
- mkdir /var/tmp/s3
- cd /var/tmp/s3
- wget http://ufpr.dl.sourceforge.net/project/s3tools/s3cmd/1.6.1/s3cmd-1.6.1.tar.gz
- tar -xf s3cmd-1.6.1.tar.gz
- cd s3cmd-1.6.1
- sudo python setup.py install
- cd /var/tmp
- sudo rm s3 -rf
- s3cmd --configure
- s3cmd ls
- s3cmd la
- s3cmd get s3://bucket_name//object_name
- s3cmd get s3://bucket_name/
