Configure Logs with CloudWatch

1) . Download CloudWatch Agent
wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb

2). Configure CloudWatch Agent
sudo dpkg -i -E ./amazon-cloudwatch-agent.deb
sudo systemctl status amazon-cloudwatch-agent

3).  Configure Log files to be shipped in
sudo nano /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json

4). sudo systemctl start  amazon-cloudwatch-agent

5). Download OTEL wget https://aws-otel-collector.s3.amazonaws.com/ubuntu/amd64/latest/aws-otel-collector.deb

6). Start 
sudo dpkg -i -E ./aws-otel-collector.deb

sudo /opt/aws/aws-otel-collector/bin/aws-otel-collector-ctl  -a start
sudo /opt/aws/aws-otel-collector/bin/aws-otel-collector-ctl  -a status

7). Download OTEL jar

wget https://github.com/aws-observability/aws-otel-java-instrumentation/releases/latest/download/aws-opentelemetry-agent.jar

8).  When Miroservices are getting strted include the OTEL Jar

nohup java -Xms256m -Xmx512m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./java_pid.hprof -javaagent:/home/ubuntu/AIOPs_Hackathon_Lab_Application/aws-opentelemetry-agent.jar -jar /home/ubuntu/AIOPs_Hackathon_Lab_Application/microservices/discovery-service/discovery-service-0.0.1-SNAPSHOT.jar -c /opt/aws/aws-otel-collector/etc/config.yaml > discovery-service.log 2>&1 &

nohup java -Xms256m -Xmx512m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./java_pid.hprof -javaagent:/home/ubuntu/AIOPs_Hackathon_Lab_Application/aws-opentelemetry-agent.jar -jar /home/ubuntu/AIOPs_Hackathon_Lab_Application/microservices/api-gateway/api-gateway-0.0.1-SNAPSHOT.jar -c /opt/aws/aws-otel-collector/etc/config.yaml > api-gateway.log 2>&1 &

nohup java -Xms256m -Xmx512m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./java_pid.hprof -javaagent:/home/ubuntu/AIOPs_Hackathon_Lab_Application/aws-opentelemetry-agent.jar -jar /home/ubuntu/AIOPs_Hackathon_Lab_Application/microservices/location-service/location-service-0.0.1-SNAPSHOT.jar -c /opt/aws/aws-otel-collector/etc/config.yaml > location-service.log 2>&1 &

nohup java -Xms256m -Xmx512m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./java_pid.hprof -javaagent:/home/ubuntu/AIOPs_Hackathon_Lab_Application/aws-opentelemetry-agent.jar -jar /home/ubuntu/AIOPs_Hackathon_Lab_Application/microservices/car-service/car-service-0.0.1-SNAPSHOT.jar -c /opt/aws/aws-otel-collector/etc/config.yaml > car-service.log 2>&1 &

nohup java -Xms256m -Xmx512m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./java_pid.hprof -javaagent:/home/ubuntu/AIOPs_Hackathon_Lab_Application/aws-opentelemetry-agent.jar -jar /home/ubuntu/AIOPs_Hackathon_Lab_Application/microservices/reservation-service/reservation-service-0.0.1-SNAPSHOT.jar -c /opt/aws/aws-otel-collector/etc/config.yaml > reservation-service.log 2>&1 &

9). Create IAM role and provide EC2 CloudWatch Full access 





