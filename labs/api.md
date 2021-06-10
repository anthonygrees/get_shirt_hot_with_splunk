# Splunk API Commands
  
[Back to the Lab Index](../README.md#get-shirt-hot-with-splunk)
  
### DMC API Commands
  
Create HEC Token. 
```bash
curl -k -u admin:your_password -X POST -H "Content-Type: application/json" https://sh-i-023ea2e672f8a5a78.csms-oslbm8-42720.stg.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http -d '{"name":"SDREST1", "description":"token created via REST", "index":"main", "sourcetype":"json_no_timestamp"}' 
```
  
List all HEC Tokens
```bash
curl -k -u admin:your_password https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http
```
  
List HEC Token by Name
```bash
curl -k -u admin:your_password https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http/SDREST1
```
  
Disable HEC Token
```bash
curl -k -u admin:your_password -H "Content-Type: application/json" https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http/SDREST1 -d '{"disabled":"true"}'
```
  
Enable HEC Token
```bash
curl -k -u admin:your_password -H "Content-Type: application/json" https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http/SDREST1 -d '{"disabled":"false"}'
```
  
Update HEC Token
```bash
curl -k -u admin:your_password -H "Content-Type: application/json" https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http/SDREST1 -d '{"description":"Updated Description"}'
```
  
Delete HEC Token
```bash
curl -k -u admin:your_password -X DELETE https://customer_splunk_url_name.splunkcloud.com:8089/services/dmc/config/inputs/__indexers/http/SDREST1
```
  
  
[Back to the Lab Index](../README.md#get-shirt-hot-with-splunk)
  
