# Infrastructure				
## AWS Zones				
Identify your zones here				
zone 1: "us-east-2a", "us-east-2b"				
zone 2: "us-west-1a","us-west-1c"				
				
## Servers and Clusters				
				
### Table 1.1 Summary				
Asset	Purpose	Size	Qty	DR
------------	-------------------	------------------------------------------------------------------------	-----------------------------------------------------------------	--------------------------------------------------------------------------------------------------------------
Asset name	Brief description	AWS size eg. t3.micro (if applicable, not all assets will have a size)	Number of nodes/replicas or just how many of a particular asset	Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere
Virtual machine (VM)	EC2 instances	t3.micro	3	Deployed in DR
Kubernetes cluster	EKS		2	Deployed in DR
VPC				Created in multiple locations
Application load balancer	Amazon ELB			Deployed to DR
SQL cluster	Amazon RDS		2 (in each cluster)	Replicated in primary and secondary zones
### Descriptions				
More detailed descriptions of each asset identified above.				
* Each VM has 3 instances (EC2)				
* Each Kubernetes cluster has 2 nodes (EKS)				
* The VPC has IPs in multiple availability zones (VPC)				
* An application load balancer in each region (ALB)				
* 2 instance nodes for each SQL cluster are present (primary and secondary clusters) and each cluster has multiple availability zones				
## DR Plan				
### Pre-Steps:				
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.				
1. Prevent configuration drift: Ensuring both primary and secondary sites are configured the same				
2. Use infrastructure as code (IaC) like Terraform to deploy the recovery/secondary assets to DR site for successful failover in case of disaster				
## Steps:				
You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region				
1. Point your DNS to your secondary region
Point to the load balancers of the secondary region where the alternative clusters are hosted using DNS VIP pointing to secondary region.

2. Failover your database replication instances (SQL instances) to another region
Manually force the secondary region to become primary at the database level, or
Automatically failover the database by health checks