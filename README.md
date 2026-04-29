\# **DNS Log Analysis Using Splunk SIEM**



\# **Project Overview :**



This project demonstrates how to \*\*collect, forward, and analyze DNS logs using Splunk SIEM\*\* in a home lab environment.



A DNS server was configured on an \*\*Ubuntu Virtual Machine\*\*, and logs were forwarded using \*\*Splunk Universal Forwarder\*\* to \*\*Splunk Enterprise running on Windows host system\*\*.



The goal was to monitor DNS traffic, identify suspicious queries, and perform security analysis.





\# **Lab Architecture :**



Ubuntu VM (BIND9 DNS Logs)

&#x20;       ↓

Splunk Universal Forwarder

&#x20;       ↓

Windows Host (Splunk Enterprise)





\# **Technologies Used :**



1.Splunk Enterprise



2.Splunk Universal Forwarder



3.Ubuntu Linux VM



4.Oracle VirtualBox



5.BIND9 DNS Server



6.Windows Host Machine



7.GitHub







\# **Project Setup :**



**1.Splunk Enterprise Setup (Windows)**



Installed Splunk Enterprise



Enabled receiving port:





9997









**2. Ubuntu VM Setup :**



Installed required packages:



sudo apt update

sudo apt install bind9 dnsutils -y







**3.DNS Logging Enabled :**



Configured BIND9 query logging:



/var/cache/bind/query.log







**4. Splunk Forwarder Configured :**



Added monitor:



sudo /opt/splunkforwarder/bin/splunk add monitor /var/cache/bind/query.log



Added forward server:



sudo /opt/splunkforwarder/bin/splunk add forward-server <Windows-IP>:9997



Restarted forwarder:



sudo /opt/splunkforwarder/bin/splunk restart







**🌐 DNS Traffic Generated**



nslookup google.com 127.0.0.1

nslookup facebook.com 127.0.0.1

nslookup youtube.com 127.0.0.1

nslookup maliciousdomain.com 127.0.0.1









🔎 **Splunk Search Queries :**



**View DNS Events**



index=\* "query:"



**Top Queried Domains**



index=\* "query:" | rex field=\_raw "query:\\s(?<domain>\[^\\s]+)" | top domain



**Count by Domain**



index=\* "query:" | rex field=\_raw "query:\\s(?<domain>\[^\\s]+)" | stats count by domain



**Search Suspicious Domain**



index=\* maliciousdomain.com







📊 **Security Findings :**  



✅ Successfully centralized DNS logs into Splunk

✅ Identified top queried domains

✅ Detected suspicious domain requests

✅ Improved DNS visibility for SOC monitoring

✅ Demonstrated real SIEM workflow







📸 **Screenshots :**



Look at the each screenshots in /screenshots folder:



* splunk-dashboard.png



* dns-query-results.png



* top-domains.png



* suspicious-domain.png



* ubuntu-dns-log.png





🎯 **Learning Outcome**



This project helped me understand:



* SIEM fundamentals
* 
* Log forwarding architecture
* 
* DNS threat monitoring
* 
* Splunk SPL queries
* 
* SOC analyst workflow
* 







👨‍💻 **Author :**



Thajul Akber



Cybersecurity Enthusiast | SOC Analyst  | Cybersecurity Analyst | Penetration Tester







