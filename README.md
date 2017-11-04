# Packer-AwsLogs

Packer cripts to build AMI's with syslogs going to Cloudwatch.

Generic Ubuntu and Windows examples provided.
```
packer build -var 'aws_profile=default' windows.json
packer build -var 'aws_profile=default' ubuntu.json
```

Note: Packer for windows requires the winrm port 5986 open.

### Resources
* http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_GettingStarted.html
  * Ubuntu example referenced - http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/QuickStartEC2Instance.html
  * Windows example referenced - http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/QuickStartWindows20082012.html
* https://autozane.com/automating-aws-cloudwatch-logs-on-ubuntu/

### To manually install

Amazon Linux
```bash
# Configure CloudWatch logs
sudo yum -y install awslogs
sudo service awslogs start
sudo chkconfig awslogs on
# Edit /etc/awslogs/awslogs.conf and /etc/awslogs/awscli.conf
sudo service awslogs restart
```
Ubuntu
```bash
# Configure CloudWatch logs
curl https://s3.amazonaws.com//aws-cloudwatch/downloads/latest/awslogs-agent-setup.py -O
chmod +x ./awslogs-agent-setup.py
sudo ./awslogs-agent-setup.py -n -r us-east-1
```
Windows
RDT with a SSH bastion
```
ssh -4 -N -L 3389:<instance ip>:3389 ubuntu@<bastion dns>

rdesktop localhost -u Administrator -p password -g 90%
```
```shell
# Configure CloudWatch logs
# Create  `C:\Program Files\Amazon\SSM\Plugins\awsCloudWatch\AWS.EC2.Windows.CloudWatch.json`
Restart-Service AmazonSSMAgent
```
