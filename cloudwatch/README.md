# INSTALL AMAZON CLOUDWATCH AGENT
```
wget https://s3.amazonaws.com/amazoncloudwatch-agent/centos/amd64/latest/amazon-cloudwatch-agent.rpm
rpm -i amazon-cloudwatch-agent.rpm
```

# INSTALL AWSCLI

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

# CONFIGURE 

```
aws configure --profile AmazonCloudWatchAgent
```

# RUN WIZARD
```
/opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
```

```
[root@ip-10-0-1-170 logs]# /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
================================================================
= Welcome to the Amazon CloudWatch Agent Configuration Manager =
=                                                              =
= CloudWatch Agent allows you to collect metrics and logs from =
= your host and send them to CloudWatch. Additional CloudWatch =
= charges may apply.                                           =
================================================================
On which OS are you planning to use the agent?
1. linux
2. windows
3. darwin
default choice: [1]:
1
Trying to fetch the default region based on ec2 metadata...
Are you using EC2 or On-Premises hosts?
1. EC2
2. On-Premises
default choice: [1]:
1
Which user are you planning to run the agent?
1. root
2. cwagent
3. others
default choice: [1]:
1
Do you want to turn on StatsD daemon?
1. yes
2. no
default choice: [1]:
2
Do you want to monitor metrics from CollectD? WARNING: CollectD must be installed or the Agent will fail to start
1. yes
2. no
default choice: [1]:
2
Do you want to monitor any host metrics? e.g. CPU, memory, etc.
1. yes
2. no
default choice: [1]:
1
Do you want to monitor cpu metrics per core?
1. yes
2. no
default choice: [1]:
2
Do you want to add ec2 dimensions (ImageId, InstanceId, InstanceType, AutoScalingGroupName) into all of your metrics if the info is available?
1. yes
2. no
default choice: [1]:
2
Do you want to aggregate ec2 dimensions (InstanceId)?
1. yes
2. no
default choice: [1]:
2
Would you like to collect your metrics at high resolution (sub-minute resolution)? This enables sub-minute resolution for all metrics, but you can customize for specific metrics in the output json file.
1. 1s
2. 10s
3. 30s
4. 60s
default choice: [4]:
4
Which default metrics config do you want?
1. Basic
2. Standard
3. Advanced
4. None
default choice: [1]:
1
Current config as follows:
{
	"agent": {
		"metrics_collection_interval": 60,
		"run_as_user": "root"
	},
	"metrics": {
		"metrics_collected": {
			"disk": {
				"measurement": [
					"used_percent"
				],
				"metrics_collection_interval": 60,
				"resources": [
					"*"
				]
			},
			"mem": {
				"measurement": [
					"mem_used_percent"
				],
				"metrics_collection_interval": 60
			}
		}
	}
}
Are you satisfied with the above config? Note: it can be manually customized after the wizard completes to add additional items.
1. yes
2. no
default choice: [1]:
1
Do you have any existing CloudWatch Log Agent (http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AgentReference.html) configuration file to import for migration?
1. yes
2. no
default choice: [2]:
1
What is the file path for the existing cloudwatch log agent configuration file?
default choice: [/var/awslogs/etc/awslogs.conf]

Do you want to monitor any log files?
1. yes
2. no
default choice: [1]:
1
Log file path:
/var/log/vitalpbx/authentications.log
Log group name:
default choice: [authentications.log]

Log stream name:
default choice: [{instance_id}]
vitalpbx-{instance_id}
Log Group Retention in days
1. -1
2. 1
3. 3
4. 5
5. 7
6. 14
7. 30
8. 60
9. 90
10. 120
11. 150
12. 180
13. 365
14. 400
15. 545
16. 731
17. 1827
18. 3653
default choice: [1]:

Do you want to specify any additional log files to monitor?
1. yes
2. no
default choice: [1]:
2
Saved config file to /opt/aws/amazon-cloudwatch-agent/bin/config.json successfully.
Current config as follows:
{
	"agent": {
		"metrics_collection_interval": 60,
		"run_as_user": "root"
	},
	"logs": {
		"force_flush_interval": 5,
		"logs_collected": {
			"files": {
				"collect_list": [
					{
						"encoding": "utf-8",
						"file_path": "/var/log/asterisk/fail2ban",
						"log_group_name": "/var/log/asterisk/fail2ban",
						"log_stream_name": "fail2ban-{instance_id}",
						"retention_in_days": -1,
						"timestamp_format": "'%Y-%m-%dT%H:%M:%S%z'",
						"timezone": "LOCAL"
					},
					{
						"encoding": "utf-8",
						"file_path": "/var/log/asterisk/full",
						"log_group_name": "/var/log/asterisk/full",
						"log_stream_name": "asterisk-{instance_id}",
						"retention_in_days": -1,
						"timestamp_format": "'%Y-%m-%dT%H:%M:%S%z'",
						"timezone": "LOCAL"
					},
					{
						"encoding": "utf-8",
						"file_path": "/var/log/messages",
						"log_group_name": "/var/log/messages",
						"log_stream_name": "messages-{instance_id}",
						"retention_in_days": -1,
						"timestamp_format": "'%Y-%m-%dT%H:%M:%S%z'",
						"timezone": "LOCAL"
					},
					{
            "encoding": "utf-8",
						"file_path": "/var/log/vitalpbx/authentications.log",
						"log_group_name": "authentications.log",
						"log_stream_name": "vitalpbx-{instance_id}",
						"retention_in_days": -1,
            "timestamp_format": "'%Y-%m-%dT%H:%M:%S%z'",
            "timezone": "LOCAL"
					}
				]
			}
		}
	},
	"metrics": {
		"metrics_collected": {
			"disk": {
				"measurement": [
					"used_percent"
				],
				"metrics_collection_interval": 60,
				"resources": [
					"*"
				]
			},
			"mem": {
				"measurement": [
					"mem_used_percent"
				],
				"metrics_collection_interval": 60
			}
		}
	}
}
Please check the above content of the config.
The config file is also located at /opt/aws/amazon-cloudwatch-agent/bin/config.json.
Edit it manually if needed.
Do you want to store the config in the SSM parameter store?
1. yes
2. no
default choice: [1]:
2
Program exits now.
```

# RUN
```
amazon-cloudwatch-agent-ctl -a fetch-config   -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```

# Status
```
amazon-cloudwatch-agent-ctl -a status
{
  "status": "running",
  "starttime": "2022-06-03T12:10:49+0000",
  "configstatus": "configured",
  "cwoc_status": "stopped",
  "cwoc_starttime": "",
  "cwoc_configstatus": "not configured",
  "version": "1.247350.0b251814"
}
```

# Restart Service 
```
/bin/systemctl restart amazon-cloudwatch-agent.service
```

