# Node.js-App-Deployment-on-AWS-Elastic-Beanstalk-with-ALB-and-Nginx-Configuration
#### This GitHub repository contains the source code and documentation for a comprehensive project that provides step-by-step guidance on deploying a Node.js application on AWS Elastic Beanstalk. The deployment is enhanced with the integration of an Application Load Balancer (ALB) and Nginx.
#### The project is structured into multiple phases, each dedicated to addressing specific components of the setup process. Through these phases, users can gain insights into creating a robust and scalable Node.js environment on AWS, leveraging AWS Services for a well-optimized deployment.





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
#### Phase-1 of the project focuses on setting up asimple Node.js (Express.js) application that responds with "Hello World" to a POST request on the local machine and preparing it for deployment by compressing it into a zipped file. Here's an explanation of each step:
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










