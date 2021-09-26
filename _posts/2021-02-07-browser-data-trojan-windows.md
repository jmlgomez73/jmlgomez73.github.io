---
layout: single
title: '<span class="projects">Browser Data Trojan for Windows - Project</span>'
excerpt: "This client-server project allows the client to recompile all the information from the Chrome, Edge and OperaGX browsers and then compresses it and send it to the server via TCP to the server, although it also has the option of doing so via Stmp, on the other hand the server allows decrypting all files, including passwords, cookies, etc"
date: 2021-02-07
categories:
  - projects
tags:  
  - python
  - malware
  - exfiltrate-data
  - av-evasion
toc: true
toc_label: "Content"
toc_sticky: true
show_time: true
---

This client-server project allows the client to recompile all the information from the Chrome, Edge and OperaGX browsers and then compresses it and send it to the server via TCP to the server, although it also has the option of doing so via Stmp.

Then the server allows decrypting all files, including passwords, cookies, etc ...

## [Link to the Github repository](https://github.com/jmlgomez73/Browser-Data-Trojan-Windows)

# **LEGAL NOTICE AND DISCLAIMER**.
This project was made for the sole purpose of education and research for developers or end users, and that can help create countermeasures for current threats.
**I DO NOT** assume any responsibility for how you choose to use any of the executables/source code of any files provided.

## Getting Started

### Prerequisites ⚙️

* [Python3](https://www.python.org/downloads/).
* Libraries : ```python -m pip install -r requirements.txt```

## How it works

<a href="/assets/images/project-browser-data-trojan-windows/1.png">
    <img src="/assets/images/project-browser-data-trojan-windows/1.png">
</a>
<p align="center">Client-Server TCP Diagram</p>

<a href="/assets/images/project-browser-data-trojan-windows/2.png">
    <img src="/assets/images/project-browser-data-trojan-windows/2.png">
</a>
<p align="center">Work Flow</p>

Regarding the process for decrypting the master key used for decrypting passwords and cookies, it was based on the following scheme, from which it can be extrapolated based on how the browser encrypts and decrypts passwords and cookies, how to decrypt them.

It must be considered that each password and cookie are encrypted in the same way but individually.

<a href="/assets/images/project-browser-data-trojan-windows/3.jpg">
    <img src="/assets/images/project-browser-data-trojan-windows/3.jpg">
</a>
<p align="center">Passords and master_key Encrypt/Decrypt</p>

### Functions

* **Client** (in fact this is the client's working flow):

  * Recompilation of the following files from Chrome, Edge and OperaGX browsers:
    * Local State 
    * Login Data 
    * Cookies 
    * History 
    * Bookmarks
  * Dumpped to a directory in  ```/temp```, zipped, moved to desktop and erased upon completion (placing it on the desktop at the end avoids the need for administrator permissions to run the program.)
  * Sending the file via TCP to the chosen port, by default 5679 (client.py) to the root dir of the server.
  * Sending the file via smtp from and to the chosen email. (client_mail.py)

* **Server**:

  * Run Server (by default listening in port 5679)
  * Unpack Data (by default unpacked in ```/Data```)
  * Decrypt Passwrds and Generate a DB
  * Check Historial
  * Decrypt Cookies
  * Check Bookmarks
  * Close

Except for the bookmarks, the other decrypted data will be dumped into a new database.


## Bypassing firewalls

We need to obfuscate the code and compile it to an executable.
For that we can use *pyarmor* and *pyinstaller*
That easy in one line in the right directory : 
* If you want via TCP : ```pyarmor pack --clean -e "--onefile " client.py```
* If you want via SMTP: ```pyarmor pack --clean -e "--onefile " client_mail.py```

The resultant execuable will be placed in the ```/dist``` path.

Using this we can avoid most antivirus, this was tested in our own laboratory.

In addition, As this is an educational project, it does not matter to upload it to VirusTotal, in the event that we were cybercriminals or with intentions contrary to the objective of this project, we would never upload our executable / code to a page like this.

* [VirusTotal TCP Client](https://www.virustotal.com/gui/file/76e41fdaa189070aabdff0d125048ef6958f311bd3cda175bf7f35e2e9a38ad0/detection) 
was only detected by 5/70 antivirus. You can check the results.

* [VirusTotal STMP Client](https://www.virustotal.com/gui/file/3adadd3324593c3a952b747ffda9c105603d9753950486b13ee6b99ffa8f6498/detection) 
was only detected by 8/70 antivirus. You can check the results.


## Configuring 🔧

Modify all the parameters in the code (normally expressed as "xxxx"), guide yourself according to the comments


## Executing the code

* You can use the comand ```python -u "C:/Path/to/file.py"``` , It's necessary to have python path specified in environment variables.

* If you are using an IDE or a configured code editor just compile and run the code.

If you are using the client via TCP you will need to run the server.
And then when the client is executed the server will accept the connection and the file will be sent and received.

**You have to open the port in the router config** (In the server side), otherwise you wouldn't receive anything.

In the case of being via smtp it is not necessary to run the server, just to process and decrypt the files.


## Things to keep in mind

* The server is created to handle a single connection

## Issues

- Decrypt Edge Cookies not working because of unknown encode, not UTF-8, not windows-1251.


## Things that will be implemented in the future

- Export the rest of the decrypted files to xlsx format