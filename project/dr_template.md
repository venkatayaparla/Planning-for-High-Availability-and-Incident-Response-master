# Infrastructure

## AWS Zones
Identify your zones here
us-east-1:
us-east-2:

## Servers and Clusters


### Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Asset name | Brief description | AWS size eg. t3.micro (if applicable, not all assets will have a size) | Number of nodes/replicas or just how many of a particular asset | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |

### Descriptions
More detailed descriptions of each asset identified above.

## DR Plan
### Pre-Steps:
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.

## Steps:
You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region



 # Business Continuity Requirements
 ## HA Requirements
 The business has determined the following as the minimum number of nodes for an HA/DR scenario:
- Each VM has 3 instances (EC2)
- Each Kubernetes cluster has 2 nodes (EKS)
- The VPC has IPs in multiple availability zones (VPC)
- An application load balancer in each region (ALB)

## SQL Requirements
In regards to their SQL cluster, the following requirements should be met:
- Create 2 instance nodes for each cluster (primary and secondary clusters)
- Set the backup retention window to 5 days
- Each cluster must have multiple availability zones
- zone1 will replicate to a cluster in zone2