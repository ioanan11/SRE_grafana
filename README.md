# Grafana Project

## 1. Setting up Grafana

### Step 1: Create and connect to EC2 Instance

- **Amazon Machine Image**: Ubuntu 18.04
- **Instance Type**: t2.micro
- **Instance Details**: 
	- Network: default VPC 
	- Subnet: zone 1a
	- Auto-assign Public IP: enable
- **Security group**: Create new security group and make sure to allow port 3000, 22 and 80. Also make sure you can SSH from your IP
- Create instance
- SSH connect to the instance

### Step 2: Run these commands

```
 sudo apt-get update
 sudo apt-get upgrade
 sudo apt-get install adduser libfontconfig1
 sudo apt-get update adduser libfontconfig1
 sudo wget https://dl.grafana.com/enterprise/release/grafana-enterprise_8.1.5_amd64.deb
 sudo dpkg -i grafana-enterprise_8.1.5_amd64.deb

```

### Step 3: Add new resource

- go to sources.list file: `sudo nano /etc/apt/sources.list
- after the last line add this:

```
# adding new resource for grafana package from package cloud
deb https://packagecloud.io/grafana/stable/debian/ stretch main
```
	
### Step 4: Run these commands

```
curl https://packagecloud.io/gpg.key | sudo apt-key add -
sudo wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana_5.2.4_amd64.deb
sudo apt-get install grafana
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl status grafana-server
sudo systemctl enable grafana-server.service
sudo service grafana-server start
systemctl status grafana-server.service
```

If the status is active, you have successfully installed grafana. Alternatively, run update and upgrade commands and check if you've missed any step.

### Step 5: Time to use grafana

- In the browser, use the EC2 public IP with port 3000.
- A login page should load, where you can input your credentials
	- username: admin
	- password: *****
- It will allow you to change the password 

**Note**: When you stop the instance, grafana status will not be active anymore, so we have to run the following commands:

```
sudo update-rc.d grafana-server defaults
sudo systemctl enable grafana-server.service
```

## 2. Using Grafana

### Let's connect to CloudWatch

- Go to Configuration > Data Sources > Add Data Source > CloudWatch

![alt text]()
