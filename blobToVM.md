```
S3 to Azure Blob to Azure VM Guide	

•	Verify that S3 Bucket is set up on AWS
o	Gather AWS access key and secret access key from AWS
•	Verify that Azure Storage Account is set up on Azure
o	Create “File Share”
	Storage Account Page > Overview > Under “Services” click “Files > “File Share”
•	Verify that an Azure “Data Factory” instance has been set up
•	Use Azure Data Factory “Copy Data” wizard twice
o	1st time follow wizard to copy file from S3 to Azure Blob
o	2nd time follow wizard to copy file from Azure Blob to File Share
o	(can also go straight from S3 to File Share depending on necessity using same wizard) 
o	Sample Azure Data Factory wizard to go from Blob > File Share
	Set up Data Factor instance
	Use “Copy Data” wizard
	Set up recurring pattern / start and end times for task
	Go through wizard selecting SAP Storage Blob as the input
•	Chose particular SAP dump file you want to transfer over
•	File format may give you trouble, just unselect most of the settings and it will let a simple file go through
	Output will be file system using URL from above steps, username will be “storage account name” from Access Keys tab and password
will be “storage account key” from Access Key tab
•	Path = //myaccountname.file.core.windows.net/mysharename
	Once this is done it should copy the specified blob file over to the file share at regular intervals which will be accessible
directly on the VM through the mountpoint
	If you wanted to regularly copy over from mountpoint to the local VM HD, you’ll need to do create a cron job to run a script
regularly to copy files
•	crontab –e
•	* * * * * cp /mnt/mountpoint/SAPFile /directory_you_want_to_copy_to
 
•	Set up Azure VM to have “File Share” mounted as an accessible disk
o	Install Samba to allow for mounting of “File Share” (if not installed already)
	sudo zypper install samba*
o	Make directory where “File Share” will be mounted
	sudo mkdir /mnt/mountpoint
	mountpoint can be whatever directory name you choose
o	Mount “File Share”
	sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mnt/mountpoint -o vers=3.0,user=myaccountname,
password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
	Mode=0777 provides access to all users on that VM, feel free to switch to other code that restricts access if needed
	Yellow highlights must be changed to respective values 
•	Azure Account
•	File Share name you created
•	Mount point you designated
•	Storage Account name
•	Storage account key
o	Storage Account Key can be found in Storage Account > Access Keys in Azure Console
o	Keep file share mounted after reboot – must add setting to /etc/fstab (edit file)
	//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,
password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
o	Once all the above is complete your VM will have a direct connection to a Storage File Share (mounted like another HD)
wherein you can place your SAP Dump file from blob and it will be accessible on the VM through the 
File Share directory @ /mnt/mountpoint
```

