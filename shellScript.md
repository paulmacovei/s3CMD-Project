# S3cmd on SUSE Linux Shell Script	

The following script below will install and configure S3cmd for usage on a SUSE system, just modify the below personal values (i.e. keys) to the AWS account access and secret keys and the encryption key is any kind you may choose to use.

```
#!/bin/bash

mkdir -p /var/tmp/s3
cd /var/tmp/s3

printf '#!/usr/bin/expect -f\n\nspawn s3cmd --configure\nexpect ":"\nsend "access\\n"\nexpect ":"\nsend "secret\\n"\nexpect ":"\nsend "\\n"\nexpect ":"\nsend "encryption_key\\n"\nexpect ":"\nsend "\\n"\nexpect ":"\nsend "\\n"\nexpect ":"\nsend "\\n"\nexpect "n]"\nsend "Y\\n"\nexpect "N]"\nsend "y\\n"' > expect_script

wget http://ufpr.dl.sourceforge.net/project/s3tools/s3cmd/1.6.1/s3cmd-1.6.1.tar.gz
tar -xf s3cmd-1.6.1.tar.gz
cd s3cmd-1.6.1
python setup.py install
cd /var/tmp/s3
expect expect_script
```
