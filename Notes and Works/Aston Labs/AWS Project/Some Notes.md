- S3 Bucket Script Link: s3://s3-bucket-of-mine/awslabscript.sh

#!/bin/bash
aws s3 cp https://myaws-s3-bucket12345.s3.us-east-2.amazonaws.com/awslabscript.sh /home/ec2-user/
chmod +x /home/ec2-user/awslabscript.sh
bash /home/ec2-user/awslabscript.sh
