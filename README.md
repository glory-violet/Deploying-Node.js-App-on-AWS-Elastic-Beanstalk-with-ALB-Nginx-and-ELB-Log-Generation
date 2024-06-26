# Deploying-Node.js-App-on-AWS-Elastic-Beanstalk-with-ALB-Nginx-and-ELB-Log-Generation

#### This GitHub repository contains the source code and documentation for a comprehensive project that provides step-by-step guidance on deploying a Node.js application on AWS Elastic Beanstalk. The deployment is enhanced with the integration of an Application Load Balancer (ALB) and Nginx.
#### The project is structured into multiple phases, each dedicated to addressing specific components of the setup process. Through these phases, users can gain insights into creating a robust and scalable Node.js environment on AWS, leveraging AWS Services for a well-optimized deployment.


## Project Architectural Overview:
### This section provides a high-level architectural overview of the project, outlining the key components, their interactions, and the overall structure.
<img src="https://github.com/glory-violet/Node.js-App-Deployment-on-AWS-Elastic-Beanstalk-with-ALB-and-Nginx-Configuration/assets/137056419/bed90171-335b-4c14-8dc0-8af301eb7ac6" alt="Image Description" width="900" height="500">



## Project - List Of Applications Used:
#### 1. [Express.js] - A web application framework for Node.js used to build the simple "Hello World" application.
#### 2. [npm] (Node Package Manager) - Used for managing dependencies and initializing the project.
#### 3. [AWS] Management Console - Used for creating and managing resources on Amazon Web Services (AWS).
#### 4. [AWS Elastic Beanstalk] - A fully managed service that makes it easy to deploy and run applications in multiple languages.
#### 5. [AWS EC2] (Elastic Compute Cloud) - Provides resizable compute capacity in the cloud. Instances are used for deploying the Node.js application and configuring Nginx.
#### 6. [AWS Application Load Balancer] (ALB) - Used to distribute incoming application traffic across multiple targets, ensuring the availability and fault tolerance of applications.
#### 7. [Nginx] - A web server and reverse proxy server used to forward requests to the Node.js application.
#### 8. [nano] (Text Editor) - A command-line text editor used for editing Nginx configuration files on the EC2 instance.
#### 9. AWS Elastic Beanstalk [Health Checks] - Configured to assess the health and status of the Node.js application on Elastic Beanstalk.
#### 10. AWS Elastic Beanstalk [Logs] - Ensure that logs are being generated as expected to facilitate troubleshooting and monitoring.



# Project - Execution:
## Phase-1 
#### Phase-1 of the project focuses on setting up a simple Node.js (Express.js) application that responds with "Hello World" to a POST request on the local machine and preparing it for deployment by compressing it into a zipped file. Here's an explanation of each step:
#### Step-1.1 - Create a folder to store your application packages. Example: "Express-app-dev"
#### Step-1.2 - Run npm [init -y] to create a basic "package.json" file.
#### Step-1.3 - Create a "server.js" file and paste the provided Node.js application code. (Copy & paste the below code in the server.js file):
```bash
const express = require('express');
const app = express();
const { PORT = 3000 } = process.env;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(PORT, (err) => {
  if (err) {
    console.error(`Error starting the server: ${err}`);
  } else {
    console.log(`Example app listening on PORT ${PORT}`);
  }
});
```
#### Step-1.4 - Install the Express package using [npm install express] command. (Now you will see additional two files named: "node_modules" and "package-lock.json")
#### Step-1.5 - Verify the application is running with the command [node server.js] (By running this command you will see an output as "Example app listening on PORT 3000".
#### Step-1.6 - Zip Your Application: (Compress all the application files into a single Zip file) 
> Select all the files and right click. Select "Compress to Zip File" option. Now you will be having a Zip folder.

#### Now your application is ready to be deployed on "AWS Elastic Beanstalk"




----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Phase-2 
#### Phase-2 of this project guides you through the process of creating an Elastic Beanstalk application, setting up the environment with the necessary configurations, uploading the Node.js application code, and ensuring a successful deployment verified through the provided domain URL.
#### Step-2.1 - Create or log in to the AWS Management Console.


#### Step-2.2 - Navigate to Elastic Beanstalk, in the AWS Management Console.
#### Step-2.3 - Click on "Create Application" 
#### Step-2.4 - Select "Web Server Environment"
#### Step-2.5 - Define the application name. example: "Express-App"
#### Step-2.6 - Under "Managed platform", select "Node.js" as the platform from the drop down menu. (Specify Node.js as the runtime platform for your application.)
#### Step-2.7 - Under "Application Code" section, select "Upload your Code" 
#### Step-2.8 - Enter the "Version Label". Example: "Express-01"
#### Step-2.9 - Select "Local File" option
#### Step-2.10 - Click on "Choose File" option, and upload the zip file.
#### Step-2.11 - Scroll down and select "Single Instance (Free-tier eligible), then click on "NEXT"



#### Step-2.12 - Under "Service Access" section, Specify the IAM role for service access.
#### Step-2.13 - Click on "Use an existing service role" 
#### Step-2.14 - Select "aws-elasticbeanstalk-service-role" from the drop menu.



#### Step-2.15 - Select an existing EC2 key pair or create a new one with SSH port: 20 permissions. This key pair is crucial for securely connecting to the EC2 instance that Elastic Beanstalk will create.  
> For this demo I have created a new Security Group with the name "Express-SG".



#### Step-2.16 - Create a new EC2 instance profile (This will allow EC2 Instance to generate log files)
> #### Step-2.16.1 - Open a new tab or window in the AWS Management Console, Navigate to IAM (Identity and Access Management).
> #### Step-2.16.2 - In the IAM dashboard, click on "Roles" in the left navigation pane.
> #### Step-2.16.3 - Click the "Create role" button.
> #### Step-2.16.4 - In the "Select type of trusted entity" step, choose "AWS service" as the entity type.
> #### Step-2.16.5 - In the "Choose the use case" step, scroll down or use the search bar to find and select "Elastic Beanstalk."
> #### Step-2.16.6 - In the "Permissions" step, attach the policy "AWSElasticBeanstalkFullAccess" to grant full access to Elastic Beanstalk resources.
> #### Step-2.16.7 - Provide a meaningful name for the IAM role, such as "Express-Role"
> #### Step-2.16.8 - Review the role details, and click "Create role" to finalize.
> #### Step-2.16.9 - Navigate back to the Elastic Beanstalk Configuration screen
> #### Step-2.16.10 - Refresh and select the "Express-Role"




----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Phase-3
#### Phase-3 of this project guides you set up an Application Load Balancer for your Elastic Beanstalk deployment
#### Phase-3.1 Open a new tab in the AWS Management Console and navigate to the EC2 section.
#### Phase-3.2 In the EC2 Dashboard, find and select the "Load Balancers" option in the left navigation pane.
#### Phase-3.3 Click on the "Create Load Balancer" button to initiate the process of creating a new load balancer.
#### Phase-3.4 Choose the type of load balancer. In this case, select "Application Load Balancer" and click on the "Create" button.
#### Phase-3.5 Define a Name to the ALB. Example: "Epress-ALB".
#### Phase-3.6 Choose the subnets where the load balancer should distribute traffic.
#### Phase-3.7 Leave all other settings as default.


#### Phase-3.8 Under "Listeners and Routing" section, click on "Create Target Group".
#### Phase-3.9 Choose the target type as "Instance" to direct traffic to EC2 instances.
#### Phase-3.10 Scroll down and define Target Group "Name". Example: "Express-TG".
#### Phase-3.11 Define the health check path ("/health") to monitor the health of instances.
#### Phase-3.12 Click on "NEXT".


#### Phase-3.13 Under "Register Targets", select the available instances.
#### Phase-3.14 Choose the instances that should be registered with the target group.
#### Phase-3.15 Click on "Include as pending below".
#### Phase-3.16 Scroll down and click on "Create target group".


#### Phase-3.17 Configuring Elastic Beanstalk Health Checks at /health in the "server.js" Application
> Modify the application code (express.js file) to include a dedicated health check endpoint at /health.
```bash
// Example Express.js route for health checks
app.get('/health', (req, res) => {
  res.json({ status: 'OK' });
});
```



----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Phase-4 
#### Phase-4 of this project guides you Set up Nginx as Reverse Proxy," the focus is on configuring Nginx to act as a reverse proxy for your Node.js application deployed on Elastic Beanstalk.
#### Phase-4.1 Access the AWS Management Console and go to the EC2 service.
#### Phase-4.2 Choose the specific EC2 instance that hosts your Node.js application.
#### Phase-4.3 Click on "Connect"
#### Phase-4.4 Select "EC2 Instance Connect" option.
#### Phase-4.5 Click on "Connect"


#### Phase-4.6 Once connected, change into the root user:
```bash
sudo su
```

#### Phase-4.7 locate the Nginx Configuration Files at /etc/nginx/nginx.conf
```bash
cd /etc/nginx/conf.d/
```

#### Phase-4.8 Before making any changes, create a backup of the existing Nginx configuration in Real-Time scenario.
> Use the below command to create a backup:
```bash
sudo cp default.conf default.conf.backup
```


#### Phase-4.9 Edit the Nginx configuration file in nano editor
```bash
sudo nano conf.d
```

#### Phase-4.10 Replace the existing contents with the provided Nginx configuration code.
```
server {
    listen 80;

    location / {
        proxy_pass http://localhost:3000;  # Assuming your Node.js app runs on port 3000
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    location /health {
        proxy_pass http://localhost:3000/health;  # Assuming your health check route is /health
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    # Add any additional configuration as needed
}
```

#### Phase-4.11 Press CTRL + O to save changes and CTRL + X to exit.


#### Phase-4.12  Restart the Nginx server 
```bash
sudo service nginx restart
```

#### Phase-4.13 Test the Setup
Access your Elastic Beanstalk environment and trigger requests.
Verify that Nginx forwards requests to your Node.js application.
Access the main application (e.g., http://your-app-name.elasticbeanstalk.com).
Access the health check route (e.g., http://your-app-name.elasticbeanstalk.com/health).





----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Phase-5 
#### Phase-5 "Ensure 200 Responses on Health Checks," the primary goal is to confirm that the Application Load Balancer (ALB) returns 200 responses on health checks, specifically at the configured /health route.
#### Phase-5.1 Navigate to the Application Load Balancer in AWS Management Console 
#### Phase-5.2 Choose the specific Application Load Balancer associated with your Elastic Beanstalk environment.
#### Phase-5.3 Under the "Description" tab, click on "Target Groups" section
#### Phase-5.4 In the target details, check information about health checks
#### Phase-5.5 Ensure that the ALB is returning 200 responses






----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Phase-6 
#### Phase-6 of the project focuses on "Obtaining Request Logs," the objective is to access and review the request logs for your Node.js application deployed on Elastic Beanstalk.
Navigate to the Elastic Beanstalk Console
Go to the environment and click on the "Logs" tab
Click on "Request Logs" - Full (This will generate a downloaded log file)
Download and examine the logs for any entries or errors specifically related to health checks.
> The logs provide valuable information about the application's performance, errors, and health check results.


## Project Conclusion:
#### this project has successfully guided you through the process of setting up a Node.js application on AWS Elastic Beanstalk, incorporating an Application Load Balancer (ALB) and using Nginx as a reverse proxy.

#### The project was divided into multiple phases, each addressing specific aspects of the deployment.

#### By successfully completing these phases, you've gained hands-on experience in deploying and configuring a Node.js application on AWS Elastic Beanstalk, enhancing its scalability and reliability with features like ALB and Nginx. This project equips you with valuable skills for deploying and managing web applications in a cloud environment.

--------------------------------------------------------THANK YOU------------------------------------------------------








