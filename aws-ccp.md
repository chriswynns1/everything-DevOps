# AWS Certified Cloud Practitioner
## Resources
- [Great reddit post with many resources](https://www.reddit.com/r/AWSCertifications/comments/1d1xg1p/aws_certified_cloud_practitioner_clfc02_ccp/?share_id=QpAk_O3IN3qWkf9nX2zZw&utm_content=1&utm_medium=android_app&utm_name=androidcss&utm_source=share&utm_term=1)
- [Exam Guide (Amazon)](https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf)

## Cert Roadmap
- Cloud Practitioner -> Solutions Architect -> Developer -> DevOps Engineer

## Notes
- 4 domains:
  1. (24%) Cloud Concepts
  2. (30%) Security / Compliance
  3. (34%) Cloud Technology / Services
  4. (12%) Billing, Pricing, Support

- Passing grade: 700/1000
- ~70% to pass (scaled scoring)
- 65 questions
  - 50 scored, 15 _unscored_
  - NO PENALTY for wrong answeres
- Format: multiple choice, multiple answer
- 1.5 hours, ~1.5min per q
- Exam time: 90mins
- Just show up 30 minutes early
- Cert is valid for 36 months (3 yrs)

### Public Cloud:
- _everything_ is built on the CSP (aka cloud-native or cloud first in this context)
- fully utilize cloud computing
- dropbox, squarespace, startups
### Private Cloud: 
- everything built on company's datacenters (on-prem)
- deploying resources on-prem, using virtualiztion / resource management tools
- strict regulatory compliance or sheer size of org
- public sector, hospitals, insurance companies, etc.
### Hybrid: 
- both. mix of on-prem and cloud
- banks, fintech, investment management, legacy on-prem
- cross-cloud: multiple cloud providers (multi-cloud)
  - ex: Azure Arc: deploy containers for K8s in GCP and AWS EKS
  - ex: Anthos (GCP's version of Arc)
  - These are known as control planes

### IAM, Roles, Permissions, oh my!
- root is always email
  - don't use this regularly
- IAM is account ID or account alias
- always add MFA
- AdministratorAccess policy lets you do pretty much anything root can do
- PowerUserAccess
  - same as above, but can't modify users

### Regions
- geographically distinct locations w/ 1+ availability zones
If you're choosing a region, here's what to consider:
1. What regulatory compliance does this region meet?
2. What's the cost of AWS services in this region?
3. What AWS services are available in this region?
4. What is the distance or latency to my end-users?

### Availability Zones
- phyiscal location made up of one or more datacenters
- each REGION usually has 3 AZs
- datacenters are close enough to provide low latency
- best practice to run workloads in 3 AZs, in case 1 or 2 datacenters fail
  - (HA)
- all traffic is encrypted
- 60mi within each other

### Fault Tolerance
- fault domain = section of network that is vulnerable to damage if a critical device or system fails
  - if a failure occurs, it will not cascade outside (limits damage)

### Global Network
- the backbone of AWS
