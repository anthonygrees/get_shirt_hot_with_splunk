# How Indexing Works
  
### About
When we think about log events life cycle in Splunk, we can think about:  
1. Input stage - how to collect data  
2. Indexing stage - processes to parse data and ingest them to Splunk Database    
3. then, how to keep data in database(hot->Warm->Cold->Freezing)   
In Splunk's doc or presentations, Input and Indexing stages are often explained as a topic of Getting Data In. 
  
### Pipelines and Queues
Data in Splunk moves through the data pipeline in phases. Input data originates from inputs such as files and network feeds. As it moves through the pipeline, processors transform the data into searchable events that encapsulate knowledge.  
  
image
  
