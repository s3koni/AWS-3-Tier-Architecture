# **A 3-Tier Architecture on AWS**

Much like the building plans of a house, we must first design the system that we wish to build on AWS. The above blueprint is a system that consists of 3 layers, namely:
1. The Web Layer, which is the front end of the product
2. The Application Layer, which is the backend of the product
3. The Database/Storage.

These 3 items make up all the components used to build this Architecture on AWS. Each of these layers function differently but have a common goal which is to keep the flow of the system going and to satisfy the end users’ conditions.

Resources Used: 
- Amazon VPC
- Amazon EC2
- Amazon RDS (with high availability)
- ELB (Elastic Load Balancing)

## The Web Layer
This layer consists of the following components:
- Two EC2 webservers, both placed in a public subnet for public access to the internet both optimized for autoscaling. The reason for two servers is availability.
- An Elastic Load Balancer (ELB) to help adjust the traffic between the two servers for performance efficiency.

## The App Layer
This layer contains two app servers as well, but in this case, they are placed in 
private subnets because we do not want public internet access, and by implication, it can only be accessed through the back-end. This layer also has an ELB controlling the traffic between the two servers for performance efficiency.

## The Database
The database service used in this case study for the storage layer is the multi AZ Relational Database Services for MySQL (RDS MySQL)

## How it Works
- When a request is sent from the user to the website, the user sees only the user interface and is able to take actions like sign in or call/search for a particular file or files etcetera.
- The request goes through the internet gateway, to the elb, which is capable of determining which instances should be best suited for handling that particular request, based on metrics.
- When the elb is triggered, it logs every action it takes to Amazon Cloudwatch where it can be monitored from the CouldWatch dashboard in the AWS management console.
- The webserver then signals the same web elb, which in turn triggers the app elb, and as a result, the appservers can communicate with the dbs when there is need for data to be called or used.
- The application layer queries the database through the elb for efficiency, and sends the data back to the web layer which then processes it to visual content for the user to see.
- These components have been established in another region to further scale for availability and also to achieve greater fault tolerance.

![The image shows the visual description of all that is described in the 3-tier architecture.](src=https://github.com/s3koni/AWS-3-Tier-Architecture/blob/main/architecture%20schematics.jpg)
