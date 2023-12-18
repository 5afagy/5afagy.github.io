---
title: Intro to Logs
date: 2023-12-17 18:32:00 -0500
categories: [Write-Ups]
tags: [Security Analyst]
image:
  path: https://github.com/5afagy/5afagy.github.io/assets/115117722/6c009776-24bd-41da-a095-69d9ee9c704d

---


## Introduction:
In the dynamic world of cybersecurity, our latest challenge beckons—an in-depth exploration into a series of web attacks. Our objective: to meticulously dissect the logs and unravel the intricacies of the tactics employed by an adversary. Join us in this investigative journey by downloading the Challenge Files, secured with the password 'infected.'<br>

## Probing the Logs:

To initiate the investigation, we deploy potent tools such as Splunk, View Logger, or any proficient log organization program. My approach involves a hands-on inspection of manual logs using a text editor and the Linux terminal.

```bash
cat access.log | awk '{print $12 , $13 }' | head -n 40
```
![Screenshot_2023-12-18_14_09_42](https://github.com/5afagy/5afagy.github.io/assets/115117722/5edb01cf-c501-48b8-b1ac-02fc4117d603)


This command facilitates the identification of user agents in header requests, a pivotal step in comprehending the attacker's tools and methods.
Unveiling the Attacker's Tactics:

## Web Reconnaissance:
- Targeting a `Macintosh` user with IP `192.168.199.1`.
```log
192.168.199.1 - - [20/Jun/2021:12:35:40 +0300] "GET /icons/blank.gif HTTP/1.1" 200 148 "http://192.168.199.5/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:89.0) Gecko/20100101 Firefox/89.0"
```
<br>

- The attacker leveraged `Nikto/2.1.6`, originating from IP `192.168.199.2`.
```log
192.168.199.2 - - [20/Jun/2021:12:36:24 +0300] "GET /bwapp/4RaXX5Ac.exe HTTP/1.1" 404 300 "-" "Mozilla/5.00 (Nikto/2.1.6) (Evasions:None) (Test:map_codes)"
```

![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/02f40489-1f06-401d-b68a-17c2869c0cde)

Answer to the first question: `nikto`


## Directory Listing Discovery:
- Log entries indicate directory listing discovery, with emphasis on results returning a status code of 200.


Answer to the second question: `directory brute force`

## Login Brute Force:
- The third attack involved a successful login brute force, evidenced by the response code 200.

Answer to the third question: `Brute Force`

Answer to the fourth question: `Yes`

## Code Injection:
    Attempting code injection using a PHP file accepting a parameter (url).
    The successful payload executed was %22%22;%20system(%27whoami%27).

Answer to the fifth question: `code injection`

Answer to the sixth question: `whoami`

## Establishing Persistency:
    Ensuring continuous access, the attacker added a backdoor using the payload %27net%20user%20hacker%20asd123!!%20/add%27.

Answer to the seventh question: `%27net%20user%20hacker%20asd123!!%20/add%27`

## Conclusion:

Our exploration of these logs has revealed a sequence of strategic maneuvers by the attacker, offering insights into the tools employed and the success of each malicious action.<br>
This investigation underscores the critical role of thorough log analysis in fortifying cybersecurity defenses.
