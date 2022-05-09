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
Application load balancer	Amazon ALB			Deployed to DR
SQL cluster	Amazon RDS		2 (in each cluster)	Replicated in primary and secondary zones

### Descriptions				
More detailed descriptions of each asset identified above.				

- Asset 1:
    * The service used here is AWS Elastic Cloud Compute (EC2)
    * Each Virtual Machine (VM) has 3 instances (EC2)
    * The instance size chosen here is t3.micro for each cluster
    * We have desployed the VM clusters in two regions, one primary (zone 1) and other DR (zone 1) as well

- Asset 2:
    * The service used here is AWS Elastic Kubernetes Service (EKS)
    * Each Kubernetes cluster has 2 nodes (EKS)
    * We have desployed the Kubernetes clusters in two regions as well, one primary (zone 1) and other DR (zone 1)

- Asset 3:
    * The service used here is AWS Virtual Private Cloud (VPC)
    * The VPC has IPs in multiple availability zones (VPC)
    * Here the VPC is also deployed for both primary region (zone 1) and DR region (zone 2)

- Asset 4:
    * The service used here is AWS Application Load Balancer (ALB)
    * An application load balancer has been deployed in each region (ALB)
    * ALB helps to distribute the incoming application traffic to appropriate nodes in the cluster

- Asset 5:
    * The service used here is AWS Relational Database Service (RDS)
    * Two instance nodes for each SQL cluster are present (primary and secondary clusters)
    * Each cluster has multiple availability zones
    * The Secondary cluster (Zone 2) acts as a replica cluster for Primary cluster (Zone 1)

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