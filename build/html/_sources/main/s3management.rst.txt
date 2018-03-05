* Use the following command to copy an object from Amazon S3 to your instance.

[ec2-user ~]$ aws s3 cp s3://my_bucket/my_folder/my_file.ext my_copied_file.ext


* Use the following command to copy an object from your instance back into Amazon S3.

[ec2-user ~]$ aws s3 cp my_copied_file.ext s3://my_bucket/my_folder/my_file.ext
