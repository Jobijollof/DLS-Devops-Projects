
## Task:
![task](./images/assignment2.png)

![task](./images/assignmet2i.png)


Requirements:

- AWS free tier

### Step 1: Create VPC

The first step is to create a new VPC to segment our web app resources. We will create two public subnets and two private subnets both in two different availability zones to ensure high availability.

After logging into the console locate the VPC service from the dashboard. Click “Create VPC”.

![create](./images/create-vpc1.png)

We will utilize the newly created VPC experience from AWS to auto-generate the names for our resources as well as create the subnets, route table, internet and nat gateway for us.

- Click on `VPC and More`

![ease](./images/vpc-more2.png)


Let’s call our "my-project2-vpc" project  and use the 10.10.0.0/16 network for our VPC and break that down into the following public subnets: 10.10.1.0/24, 10.10.2.0/24, and 10.10.3.0/24.


![ease](./images/vpc-more3.png)


![ease](./images/vpc-more4.png)


![ease](./images/vpc-more5.png)

### Step 2: Create Security Groups:

Now that our VPC and network resources have been created we can create a launch template that will be used with our auto-scaling group and application load balancer.

1. Create ALB security group:

- Open the EC2 service in the AWS Management Console.

- Navigate to Security Groups.

- Create a new security group for the ALB.

- Allow incoming traffic on ports 80 and 443 from any source (0.0.0.0/0).

![mine](./images/ALB-SG.png)

2. Create an ASG Security Group:

- Create another security group for the ASG.

- Configure inbound rules to only allow traffic from the ALB Security Group.

![mine](./images/ASG.png)


By configuring the inbound rule to only allow traffic from the ALB Security Group, we  are ensuring that only the Application Load Balancer can send traffic to the instances within the Auto Scaling Group (ASG). This provides a secure and controlled access mechanism for incoming requests to our ASG.


### Step 3: Launch Configuration

- Navigate to the EC2 service in the AWS Management Console.

- Click on Launch templates

![launch](./images/launch-temp.png)

- Click on Create Launch templates

![launch](./images/launch-temp2.png)

- Launch template name

- Choose an Amazon Machine Image (AMI) that includes a basic web server (e.g., Amazon Linux AMI).

- Select the t2.micro instance type.

- Configure user data script to install and configure the web server (e.g., using a startup script).

- Associate the ASG Security Group created earlier.


### Step 4: Create an Auto Scaling Group (ASG)

- Within the EC2 service, navigate to Auto Scaling Groups.

![group](./images/ASG-1.png)

- Create a new Auto Scaling Group:

- Select the Launch Configuration created earlier.

- Set the desired capacity and maximum size to 2 (to stay within the free tier).

- Choose the private subnet created in Step 1.

- Associate the ASG with the ASG Security Group.

- Enable scaling policies based on desired metrics (e.g., CPU utilization).

