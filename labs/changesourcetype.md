# Change Sourcetype.  
Should you really need to bring the data in again because the correct sourcetype needs index time parsing (splitting on sourcetype into multiple like we see a lot with firewalls and other syslog sources), I built a search to create the oneshot commands you can run
  
```bash
index=<CLIENTINDEX> 
| eval command="/opt/splunkforwarder/bin/splunk add oneshot "+source+" -index <CLIENTINDEX> -sourcetype '<NEWSOURCETYPE>' -host '<HOST>" 
| stats count by command 
| fields command
```
  
Just make sure you set the time picker to the effected times. Then export those results, create a `oneshot.sh` script and ran it.
