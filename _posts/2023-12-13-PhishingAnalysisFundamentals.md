---
title: Phishing Analysis Fundamentals
author: khafagy
date: 2023-12-12 18:32:00 -0500
categories: [Write-Ups]
tags: [Security Analyst]

---
![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/73b1601f-f63a-431f-82e8-70667094b19a)

## Introduction 
Explore the fundamentals of phishing analysis in this comprehensive journey, covering the intricacies of email addresses, delivery mechanisms, headers, body content, and various types of phishing attacks.

Explore these concepts in a hands-on way with the resources available at TryHackMe - [Phishing Analysis Fundamentals](https://tryhackme.com/room/phishingemails1tryoe).

## Task 2:  The Email Address 

In Task 2, we explore the historical context of email. The invention of the email dates back to the 1970s, marking a significant milestone in communication technology.

![Screenshot_2023-12-14_19_25_14](https://github.com/5afagy/5afagy.github.io/assets/115117722/02b9b747-a9b1-4e60-86f6-23af56f933ba)

**Answer the question:** ```1970s``` 


## Task 3:  Email Delivery 

To comprehend the nuances of various email protocols, we refer to an article. The article highlights that secure IMAP employs port 993, insecure IMAP uses port 143, secure SMTP operates on port 465, and insecure SMTP utilizes ports 587. Similarly, secure POP3 is on port 995, and insecure POP3 employs port 110.

![Screenshot_2023-12-14_19_34_32](https://github.com/5afagy/5afagy.github.io/assets/115117722/82f6df85-1825-4a34-805e-2a4a8f4fbf01)

Article Link: https://help.dreamhost.com/hc/en-us/articles/215612887-Email-client-protocols-and-port-numbers

![Screenshot_2023-12-14_21_24_25](https://github.com/5afagy/5afagy.github.io/assets/115117722/3856d5d0-204d-495f-9e41-85ed6982b0ab)

- **Secure Transport for SMTP:** Port 465
- **Insecure Transport for SMTP:** Port 587

- **Secure Transport for IMAP:** Port 993
- **Insecure Transport for IMAP:** Port 143

- **Secure Transport for POP3:** Port 995
- **Insecure Transport for POP3:** Port 110




## Task 4: Email Header Analysis

Before addressing Task 4 questions, it's imperative to read the provided article on understanding email headers, available at [Media Temple](https://mediatemple.net/community/products/all/204643950/understanding-an-email-header).

Also this [Article to view email headers](https://mediatemple.zendesk.com/hc/en-us/articles/204644060-how-do-i-view-email-headers-for-a-message).

<!--You can review this email in the `Email Samples` directory on the Desktop within the attached virtual machine. 
The email is titled `email1.eml`. 

![Screenshot_2023-12-14_21-40-48](https://github.com/5afagy/5afagy.github.io/assets/115117722/26af7e7e-b9dd-4a37-818c-067f8090b375)
--> 

Return-Path
The email address for return mail. This is the same as `Reply-To:`.

![Screenshot_2023-12-14_19_41_47](https://github.com/5afagy/5afagy.github.io/assets/115117722/c246b210-96a6-4b5e-8a83-3d5089bffcc7)

Once the email sender's IP address is found, you can search for it at `http://www.arin.net/`

![Screenshot_2023-12-14_19_42_11](https://github.com/5afagy/5afagy.github.io/assets/115117722/bb112655-ec53-4fb6-9072-67a279057daa)

![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/f4df6b8a-5dae-4d8f-94b5-b8f2ba6ffcd5)

**Q1:** ```Return-Path```  
**Q2:** ```http://www.arin.net/``` 




## Task 5: Email Body 

Task 5 requires a careful examination.

**Q1: In the above screenshots, what is the URI of the blocked image?**
Inspect the HTML code segment for the image URI.

![Screenshot_2023-12-14_21-59-44](https://github.com/5afagy/5afagy.github.io/assets/115117722/32b15a73-4dd0-4ebe-9dd6-e7631e43b058)


**Q2:** Answer within the source code

![Screenshot_2023-12-14_22-02-42](https://github.com/5afagy/5afagy.github.io/assets/115117722/c4a11889-9281-4d5d-82b7-ade0734dbbca)




In the attached virtual machine, view the information in `email2.txt` and reconstruct the PDF using the base64 data. What is the text within the PDF?

![Screenshot_2023-12-14_19_47_26](https://github.com/5afagy/5afagy.github.io/assets/115117722/9bce3333-9d72-4875-9071-8f6361d1b07a)

![Screenshot_2023-12-14_19_47_43](https://github.com/5afagy/5afagy.github.io/assets/115117722/91c23c11-9355-4f1e-b9b9-f42cb839d32d)

**Q3:** Answer using CyberChef or Terminal

We can solve it using terminal or cyberchef.

# Using terminal:

**Step 1:** Take this and open terminal and write this command ```nano encode.txt``` and `Ctrl + Shift + c` to paste and `Ctrl + x` to save.<br>

**Step 2:** run this command to echo content file and use base64 decode then redirect output to file khafagy.pdf `cat encode.txt | base64 -d > khafagy.pdf`<br>

**Step 3:** run this command to open pdf ` open khafagy.pdf `<br>

  ![Screenshot_2023-12-14_22_14_57](https://github.com/5afagy/5afagy.github.io/assets/115117722/64020a88-a0e8-4211-8171-3456db72353f)

![Screenshot_2023-12-14_22_15_01](https://github.com/5afagy/5afagy.github.io/assets/115117722/91cdc8a2-4696-4265-a224-23b7472c9222)

![Screenshot_2023-12-14_22_15_22](https://github.com/5afagy/5afagy.github.io/assets/115117722/6232f049-2833-4bcb-a635-a0329ca4e88f)

# Using CyberChef:

**Step 1:** Paste content in cyberchef <br>
**Step 2:** Drag and Drop  `From Base64`<br>
**Step 3:** Click on magic wand<br>

![Screenshot_2023-12-14_22_20_12](https://github.com/5afagy/5afagy.github.io/assets/115117722/415e770f-20f6-4ef1-9871-c528ca2bc05c)


**Step 4:** We found output PDF format, save it and open file <br>

![Screenshot_2023-12-14_22_20_15](https://github.com/5afagy/5afagy.github.io/assets/115117722/8cf9c991-e65b-4405-b0e5-deb0db439b45)

![Screenshot_2023-12-14_19_54_13](https://github.com/5afagy/5afagy.github.io/assets/115117722/e8a32234-5b0c-4eda-bd3a-065139f3cf52)




## Task 6: Types of Phishing

Upon analyzing the contents of `email3.eml`, we discover relevant information in its headers. The following details are found:

- Received: from 10.253.62.157 by atlas102.free.mail.gq1.yahoo.com
- In: Sun, 11 Jul 2021 11:48:13
- Return-Path: <support@teckbe[.]com>
- From: =?UTF-8?B?VGhhbmsgeW91ISBIb21lIERlcG90?= <support@teckbe[.]com>
- To: alexa@yahoo[.]com
- Subject: =?UTF-8?B?T3JkZXIgUGxhY2VkIDogWW91ciBPcmRlciBJRCBPRDIzMjE2NTcwODkyOTEgUGxhY2VkIFN1Y2Nlc3NmdWxseQ==?=
- Message-ID: <tkbe_204456168_28443456_28260243_2164817_269_520_5436[.]1626003191881.com[.]root@tcbe-236083[.]teckbe[.]com>
- X-Complaints-To: <abuse@teckbe[.]com>
- List-Unsubscribe: http[://]t[.]teckbe[.]com/p/?j3=EOowFcEwFHl6EOAyFcoUFVTVEchwFHlUFOo6MjL6EbTT

Check any text encoded to decode using cyberchef.


Additionally, there is a base64-encoded string. Upon decoding, we find:

```plaintext
Hqh9q7comz8ABZhkUYUnXLmXLhksUBky1IEInhysFNPo5Yl0B6oldn9/jCCe+rJUXDNpOo4W6
KQq2okdMZ8XpIvNEq5yAWboBtBlog+8qYcQPbRjcEToW4kwWdq21D9neKZR/eiiadneR6qjl+RX
YXjVaKA1bDJ1HBZFWx5TakL0hRjzSf8Q/JMVq7kZvOs6UDAwiUltSQ6SSC1KtwDc76MzqHC1bmk
ZGEH2Qm5Z6KpcQULBHj4KKynb13jBRRU5aX/aqGCMC9UIQn+YqyzMqfSz02oKd8hf8Az8pl5lWX
g4lF1c+4rhhJWlNhScA9bcQ9jZezlYaBpsaMr00Ap5XA==
```

Noting !! 


![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/a3f99f17-f28a-4abc-a2f7-56face0d98e3)


From header include  =?UTF-8?B?VGhhbmsgeW91ISBIb21lIERlcG90?= <support@teckbe[.]com>  may be base64. 

Good output: Answer Q1

![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/300e159a-11e3-4c69-947f-efe6d50463d5)


Also form this header answer Q2 => `support@teckbe[.]com`


Also subject contain `==` base64 
Subject: =?UTF-8?B?T3JkZXIgUGxhY2VkIDogWW91ciBPcmRlciBJRCBPRDIzMjE2NTcwODkyOTEgUGxhY2VkIFN1Y2Nlc3NmdWxseQ==?=

Nice, Answer Q3

![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/a1afcb77-f289-4549-8612-8353078f98ef)
 
**Q4:** What is the URL link for - CLICK HERE? (Enter the defanged URL)
Click `Ctrl + f` to search in body => CLICK  

![Screenshot_2023-12-14_20_08_23](https://github.com/5afagy/5afagy.github.io/assets/115117722/ea4de261-07c8-4907-a2da-18a5aa70d1b2)

**Reminder:** When dealing with hyperlinks and attachments, you need to be careful not to accidentally click on the hyperlink or the attachment. Upon decoding, we find answers to the following questions:

![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/9d9c2efd-0a3a-43dd-8178-cd0d2d308a61)

**Hint** There are repeat characters that you can remove from the URL. CyberChef can help you with this, along with defanging. 

![Screenshot_2023-12-14_22-56-32](https://github.com/5afagy/5afagy.github.io/assets/115117722/38894fd7-30d2-4fc8-a001-db60083c5ddb)



**Q1:** `Home Depot` <br>

**Q2:**  `support@teckbe[.]com` <br>

**Q3:**  `Order Placed : Your Order ID OD2321657089291 Placed Successfully ` <br>

**Q4:**  `hxxp[://]t[.]teckbe[.]com/p/?j3=EOo=wFacEwFHl6EOAyFcoUFVTVEchwFHlUFOo6lVTTDcATE7oUE7AUET==` <br>

---

# Tools:
- [CyberChef](https://gchq.github.io/CyberChef/)
- [Base64](https://www.baeldung.com/linux/cli-base64-encode-decode)
  
With this, we conclude the phishing attack lab. Goodbye.
