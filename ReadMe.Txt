Configure Logs with CloudWatch

1) . Download CloudWatch Agent
wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb

2). Configure CloudWatch Agent
sudo dpkg -i -E ./amazon-cloudwatch-agent.deb
sudo systemctl status amazon-cloudwatch-agent

3).  Configure Log files to be shipped in
sudo nano /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json

4). sudo systemctl start  amazon-cloudwatch-agent
