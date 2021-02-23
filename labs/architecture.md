# Splunk Architecture
  
[Back to the Lab Index](../README.md#get-shirt-hot-with-splunk)
  
### About
Splunk Validated Architectures (SVAs) are proven reference architectures for stable, efficient and repeatable Splunk deployments. Many of Splunk's existing customers have experienced rapid adoption and expansion, leading to certain challenges as they attempt to scale. At the same time, new Splunk customers are increasingly looking for guidelines and certified architectures to ensure that their initial deployment is built on a solid foundation. SVAs have been developed to help our customers with these growing needs.  
  
### Splunk Cloud Deployment
When you are chosing Splunk Cloud, all deployment decisions regarding your indexing and search topologies have already been made for you. The Splunk Cloud team will build and operate your dedicated (single-tenant) AWS environment in a way that allows for meeting Splunk's compliance
requirements and our service SLAs with you.   
  
The indexers that support your cloud environment are distributed across multiple fault domains to ensure a
highly available service within a single region.  
  
The search head(s) are deployed into their own security group. Depending on your Splunk Cloud service agreement, that will either be a single search head or a search head cluster.  
  
### Splunk Cloud Deployment Architecture
  
  
### Further Details
You can get more details on Splunk Validated Architectures [here](https://www.splunk.com/pdfs/technical-briefs/splunk-validated-architectures.pdf).
  
[Back to the Lab Index](../README.md#get-shirt-hot-with-splunk)
  
