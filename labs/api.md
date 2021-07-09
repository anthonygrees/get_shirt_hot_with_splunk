# Splunk API Commands
  
[Back to the Lab Index](../README.md#get-shirt-hot-with-splunk)
  
## About the API
The splunk cloud admin api is intended to empower the customer admins to manage their Splunk Cloud Stacks.  
  
  
## ACS
The ACS (Admin Config Service) is an external facing service that will actually handle the API requests from the Splunk Cloud Admins. The service will in-turn translate the calls to the various internal systems to honour the admins requests as required.  
  
## C02 Framework
co2 is the existing framework that manages the infrastructure that runs the splunk cloud stacks. co2 is based on the kubernetes operator model, where every stack is tracked by the Stacks (CRD) Custom Resource Definition. The splunk-cloud-operator then keeps watching these CRDs and updates the splunk stacks and their infrastructure as required to match the requested specifications in their respective CRDs.  

  
| API           | Link         |
| ------------- |:------------:|
| DMC API - Distributed Management Console     | [Link](https://github.com/anthonygrees/get_shirt_hot_with_splunk/blob/main/labs/api.md#dmc-api-commands) |
| ACS API - Admin Config Service    | [Link](https://github.com/anthonygrees/get_shirt_hot_with_splunk/blob/main/labs/api.md#acs-api-commands) |
  
### DMC API Commands
The DMC is the Distributed Management Console and provides a set of API commands.
  
  
Ensure the DMC API is available for use.  
```bash
curl -k -u admin:your_password https://CUSTOMER_NAME.splunkcloud.com:8089/services/dmc/info
```
If you get a response saying the DMC servive is ```enabled``` you can use the commands below.  
  
Create HEC Token. 
```bash
curl -k -u admin:your_password -X POST -H "Content-Type: application/json" https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http -d '{"name":"Anthony1", "description":"token created via REST", "index":"main", "sourcetype":"json_no_timestamp"}' 
```
  
List all HEC Tokens
```bash
curl -k -u admin:your_password https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http
```
  
List HEC Token by Name
```bash
curl -k -u admin:your_password https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http/Anthony1
```
  
Disable HEC Token
```bash
curl -k -u admin:your_password -H "Content-Type: application/json" https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http/Anthony1 -d '{"disabled":"true"}'
```
  
Enable HEC Token
```bash
curl -k -u admin:your_password -H "Content-Type: application/json" https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http/Anthony1 -d '{"disabled":"false"}'
```
  
Update HEC Token
```bash
curl -k -u admin:your_password -H "Content-Type: application/json" https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http/Anthony1 -d '{"description":"Updated Description"}'
```
  
Delete HEC Token
```bash
curl -k -u admin:your_password -X DELETE https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http/Anthony1
```
  
  
  
### ACS API Commands
Admin config service (ACS) commands to support operations on HEC via service.
  
Add HEC Token.  
```bash
curl --location --request POST 'admin.splunk.com/:stack/adminconfig/v1/inputs/http-event-collectors' \
--header 'Authorization: Bearer <token>' \
--data-raw '{
    “name” : “tokenname”,
    "defaultIndex": "idx",
    "defaultSource": "default_source",
    "defaultHost": "somehost.com",
    "defaultSourceType": "source_type",
    "disabled": false,
    "allowedIndexes": [
        "idx",
        "notidx"
    ]
}'
```
  
Get HEC Token.  
```bash
curl --location --request GET 'admin.splunk.com/:stack/adminconfig/v1/inputs/http-event-collectors' \
--header 'Authorization: Bearer <token>'
```
  
Get HEC Name.  
```bash
curl --location --request GET 'admin.splunk.com/:stack/adminconfig/v1/hec/newhectoken' \
--header 'Authorization: Bearer <token>'
```
  
Delete HEC Name.  
```bash
curl --location --request DELETE 'admin.splunk.com/:stack/adminconfig/v1/inputs/http-event-collectors/:hecname' \
--header 'Authorization: Bearer <token>' \
--data-raw '{}'
```
  
  
  
[Back to the Lab Index](../README.md#get-shirt-hot-with-splunk)
  
