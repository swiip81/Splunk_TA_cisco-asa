# Splunk_TA_cisco-asa
Splunk_TA_cisco-asa **optimized**

CiscoAsa logs format differ with all message ids, and the method used by the official splunk TA is really not optimized because it try to apply its 168 regex at the search time to do parsing of each line of log. Really slow on high volume of logs.

The aim of the patch here, is to append the messageId to the cisco:asa sourcetype of the log at **indextime** and then call at **searchtime** only the regex associate to that messageId.

The proposed change here can be applied to already logs indexed, but optimization will only apply to new logs indexed after patching.

Patch for :
 -  search head
 -  indexers
 -  heavy forwarders

Download original splunk TA for cisco-asa logs here :
https://splunkbase.splunk.com/app/1620/

and apply the two patches in the default folder to the offical files :

    $ patch props.conf props.patch
    $ patch transforms.conf transforms.patch
