---
title: Intro to Logs
author: khafagy
date: 2023-12-12 18:32:00 -0500
categories: [Write-Ups]
tags: [Security Analyst]

---
![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/1a06c0fc-240d-4822-8abd-ccd49d1de42d)

## Introduction

Dive into the basics of log analysis to understand how logs work, where the data comes from, and the methods used to collect it. Learn the essential principles that form the foundation of log analysis.

Explore these concepts in a hands-on way with the resources available at TryHackMe - [Introduction to Logs](https://tryhackme.com/room/introtologs#).

## Task 2 Expanding Perspectives: Logs as Evidence of Historical Activity 

**Step 1:** Start machine  
 
Upon accessing the machine, I discovered a note.txt file on the desktop. Upon inspection, I found the solution to the questions in Task 2, which involved identifying the name of the colleague who left the note on the desktop and determining the full path to the suggested log file for initial investigation.

![Screenshot_2023-12-15_00-31-21](https://github.com/5afagy/5afagy.github.io/assets/115117722/172847a4-631c-456f-afbb-2bd7e4955c8e)


---
## Task 3 Types, Formats, and Standards 

The Combined log format, includes extra fields like referrer and user agent. It's commonly used as the default logging format by Nginx.

```bash
damianhall@WEBSRV-02:/var/log/gitlab/nginx$ tail -n 10 access.log
34.253.159.159 - - [14/Dec/2023:23:08:50 +0000] "GET /7 HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -
34.253.159.159 - - [14/Dec/2023:23:08:50 +0000] "GET /_lib HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -
34.253.159.159 - - [14/Dec/2023:23:08:51 +0000] "GET /_media HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -
34.253.159.159 - - [14/Dec/2023:23:08:51 +0000] "GET /7z HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -
34.253.159.159 - - [14/Dec/2023:23:08:51 +0000] "GET /_mem_bin HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -
34.253.159.159 - - [14/Dec/2023:23:08:51 +0000] "GET /8 HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -
34.253.159.159 - - [14/Dec/2023:23:08:51 +0000] "GET /_mm HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -
34.253.159.159 - - [14/Dec/2023:23:08:51 +0000] "GET /9 HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -
34.253.159.159 - - [14/Dec/2023:23:08:51 +0000] "GET /_mmserverscripts HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -
34.253.159.159 - - [14/Dec/2023:23:08:51 +0000] "GET /96 HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -
```
In Task 2, the log file specified belongs to the web server category, evident from the log's content.

![Screenshot_2023-12-15_01-09-12](https://github.com/5afagy/5afagy.github.io/assets/115117722/7e78c58b-0de2-46e6-99a7-20acb311c628)


**Based on the list of log types in this task, what log type is used by the log file specified in the note from Task 2?** <br>

**Ans:** `Web Server Log` 

**Based on the list of log formats in this task, what log format is used by the log file specified in the note from Task 2?** <br>

**Ans:** `Combined`

---
## Task 4 Collection, Management, and Centralisation

1- Open a Terminal. <br>

2- Ensure rsyslog is Installed: You can check if rsyslog is installed by running the command: `sudo systemctl status rsyslog` <br>

3-  Create a new configuration file:`nano /etc/rsyslog.d/98-websrv-02-sshd.conf`<br>

4- Add the Configuration: Add the following lines in /etc/rsyslog.d/98-websrv-02-sshd.conf to direct the sshd messages to the specific log file: 
```
$FileCreateMode 0644 

:programname, isequal, "sshd" /var/log/websrv-02/rsyslog_sshd.log
```
5- Save and Close the Configuration File. <br>


![Screenshot_2023-12-15_01_44_57](https://github.com/5afagy/5afagy.github.io/assets/115117722/87387bd7-d395-40de-9a92-c74bf3d13a8a)

6- Restart rsyslog: Apply the changes by restarting rsyslog with the command: `sudo systemctl restart rsyslog` <br> 

7- Verify the Configuration: You can verify the configuration works by initiating an SSH connection to localhost via `ssh localhost` <br>

![Screenshot_2023-12-15_01_48_05](https://github.com/5afagy/5afagy.github.io/assets/115117722/5ae41304-2861-4dc7-abbf-f5b9edc477e2)

- Discover the file at /var/log/websrv-02/rsyslog_sshd.log as it contains username.
  `tail -n13 rsyslog_sshd.log`
  
![Screenshot_2023-12-15_01_49_52](https://github.com/5afagy/5afagy.github.io/assets/115117722/9fb97718-998c-443e-84e8-998f0afc0f24)

- Uncover the file that reveals the IP address of SIEM-02 by examining the rsyslog configuration file located at /etc/rsyslog.d/99-websrv-02-cron.conf. <br>

`cat /etc/rsyslog.d/99-websrv-02-cron.conf`

![Screenshot_2023-12-15_01_51_53](https://github.com/5afagy/5afagy.github.io/assets/115117722/a07b0671-5010-4af6-b293-0bc5e581fd81)

- Discovered this file: the logs generated in /var/log/websrv-02/rsyslog_cron.log. Determine the command being executed by the root user.
  `tail -n13 rsyslog_cron.log`
  
![Screenshot_2023-12-15_01_51_08](https://github.com/5afagy/5afagy.github.io/assets/115117722/b43cede7-2cc5-456b-ab91-519a88874473)


---
## Task 5 Storage, Retention, and Deletion 

Discovered the logrotate configuration file at `/etc/logrotate.d/99-websrv-02_cron.conf`. It contains information about the retention of old compressed log file copies and specifies the frequency of log rotation.

`cat /etc/logrotate.d/99-websrv-02_cron.conf`

![Screenshot_2023-12-15_02-39-17](https://github.com/5afagy/5afagy.github.io/assets/115117722/0cfcfe75-a8f9-4dd5-b116-23db8fab9cc8)


---
## Task 6 Hands-on Exercise: Log analysis process, tools, and techniques 
Accessing the log viewer URL : http://MACHINE_IP:8111/log?log=%2Fvar%2Flog%2Fgitlab%2Fnginx%2Faccess.log&log=%2Fvar%2Flog%2Fwebsrv-02%2Frsyslog_cron.log&log=%2Fvar%2Flog%2Fwebsrv-02%2Frsyslog_sshd.log&log=%2Fvar%2Flog%2Fgitlab%2Fgitlab-rails%2Fapi_json.log


After this click on add filter icon like this: 

![Screenshot_2023-12-15_16_49_46](https://github.com/5afagy/5afagy.github.io/assets/115117722/cbd5eaa7-8eeb-44da-87f8-1b431b5727b4)

**Answer:** `No date field`<br>


Normalisation is standardising parsed data. It involves bringing the various log data into a standard format, making comparing and analysing data from different sources easier. It is imperative in environments with multiple systems and applications, where each might generate logs in another format. 


**Answer:** `Normalisation` <br>

Log enrichment adds context to logs to make them more meaningful and easier to analyse. It could involve adding information like geographical data, user details, threat intelligence, or even data from other sources that can provide a complete picture of the event.

Enrichment makes logs more valuable, enabling analysts to make better decisions and more accurately respond to incidents. Like classification, log enrichment can be automated using machine learning, reducing the time and effort required for log analysis. 


**Answer:** `Enrichment` <br>

---

## Tools:
- [Log Viewer](https://github.com/sevdokimov/log-viewer)
- [Logrotate](https://github.com/logrotate/logrotate)
- [Nano](https://www.nano-editor.org/dist/v2.1/nano.html)
-  [Systemctl](https://www.redhat.com/sysadmin/linux-systemctl-manage-services)
  
---

In closing, remember: every log contributes to the puzzle of securing our digital world.<br>

Stay curious, stay vigilant, and keep exploring the dynamic realm of cybersecurity.
