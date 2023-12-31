# Laboratory for Penetration Testing Techniques with ffuf
1. [Introduction](#introduction)
2. [Requirements](#requirements)
   - [Update your machine](#update-your-machine)
   - [Install docker](#install-docker)
   - [Install docker-compose](#install-docker-compose)
3. [Installation](#installation)
   - [Clone git repository](#clone-git-repository)
   - [Clone SecLists git repository](#clone-seclists-git-repository)
   - [Start lab environment](#start-lab-environment)
4. [Usage](#usage)
   - [Directory Fuzzing](#directory-fuzzing)
   - [Page Fuzzing](#page-fuzzing)
   - [Directory and Page Fuzzing with Extensions](#directory-and-page-fuzzing-with-extensions)
   - [Recursive Fuzzing](#recursive-fuzzing)
   - [Parameter Fuzzing for GET and POST Requests](#parameter-fuzzing-for-get-and-post-requests)
     * [GET Parameter fuzzing](#get-parameter-fuzzing)
     * [POST Parameter fuzzing](#get-parameter-fuzzing)
   - [Value Fuzzing](#value-fuzzing)
   - [Cookie Fuzzing](#cookie-fuzzing)
   - [Token Fuzzing](#token-fuzzing)
   - [Custom Header Fuzzing](#custom-header-fuzzing)
5. [Learning Scenario](#learning-scenario)
6. [License](#license)

## Introduction
This repository is a a comprehensive resource for learning penetration testing techniques using `ffuf`. 

This repository serves as an ideal starting point for individuals or students keen on mastering web security assessment skills using `ffuf`.

---

## Requirements
Instructions on how to use the application.

### Update your machine
Update your linux machine with this command:
<div class="code-snippet">
<pre><code>sudo apt update</code></pre>
<button class="copy-button" onclick="copyToClipboard('sudo apt update')"></button>
</div>

If needed upgrade your linux machine with this command:
<div class="code-snippet">
<pre><code>sudo apt upgrade</code></pre>
<button class="copy-button" onclick="copyToClipboard('sudo apt upgrade')"></button>
</div>

Update `docker` configuration files with this command:
<div class="code-snippet">
<pre><code>sudo dpkg --configure -a</code></pre>
<button class="copy-button" onclick="copyToClipboard('sudo dpkg --configure -a')"></button>
</div>

### Install docker
Install `docker` with this command:
<div class="code-snippet">
<pre><code>sudo apt install -y docker.io</code></pre>
<button class="copy-button" onclick="copyToClipboard('sudo apt install -y docker.io')"></button>
</div>

You can skip this step if you have the requirement already installed.
Check the `docker` version with this command:
<div class="code-snippet">
<pre><code>docker-compose --version</code></pre>
<button class="copy-button" onclick="copyToClipboard('docker-compose --version')"></button>
</div>

### Install docker-compose
Install `docker-compose` on your machine with this command:
<div class="code-snippet">
<pre><code>sudo wget "https://github.com/docker/compose/releases/download/v2.23.1/docker-compose-$(uname -s)-$(uname -m)" -O /usr/local/bin/docker-compose</code></pre>
<button class="copy-button" onclick="copyToClipboard('sudo wget "https://github.com/docker/compose/releases/download/v2.23.1/docker-compose-$(uname -s)-$(uname -m)" -O /usr/local/bin/docker-compose')"></button>
</div>

Test docker installation by running this command:
<div class="code-snippet">
<pre><code>docker run hello-world</code></pre>
<button class="copy-button" onclick="copyToClipboard('docker run hello-world')"></button>
</div>

You can skip this step if you have the requirement already instaled.
Check the `docker` version with this command:
<div class="code-snippet">
<pre><code>docker-compose --version</code></pre>
<button class="copy-button" onclick="copyToClipboard('docker-compose --version')"></button>
</div>

Change access permissions to executable with this command:
<div class="code-snippet">
<pre><code>sudo chmod +x /usr/local/bin/docker-compose</code></pre>
<button class="copy-button" onclick="copyToClipboard('sudo chmod +x /usr/local/bin/docker-compose')"></button>
</div>

---

## Installation
Steps for installing and running the web application.

### Clone git repository
Clone the project from the github repository to your direcotry on your linux machine using this command:
<div class="code-snippet">
<pre><code>sudo git clone https://github.com/nicolasbelz/ffufapp.git</code></pre>
<button class="copy-button" onclick="copyToClipboard('sudo git clone https://github.com/nicolasbelz/webapp.git')"></button>
</div>

### Clone SecLists git repository
Clone the `SecLists` github repository to `/opt` on your linux machine using this command:
<div class="code-snippet">
<pre><code>cd opt
sudo git clone https://github.com/danielmiessler/SecLists.git</code></pre>
<button class="copy-button" onclick="copyToClipboard('cd opt
sudo git clone https://github.com/danielmiessler/SecLists.git')"></button>
</div>

### Start lab environment
Open the terminal in the cloned project directory and start the web application using this command:
<div class="code-snippet">
<pre><code>sudo docker-compose up -d</code></pre>
<button class="copy-button" onclick="copyToClipboard('sudo docker-compose up -d')"></button>
</div>

Access the web application on your browser via `localhost`:
<div class="code-snippet">
<pre><code>http://localhost</code></pre>
<button class="copy-button" onclick="copyToClipboard('http://localhost')"></button>
</div>

If the web application is not accessible check if `docker` is enabled by running this command:
<div class="code-snippet">
<pre><code>sudo systemctl status docker</code></pre>
<button class="copy-button" onclick="copyToClipboard('sudo systemctl status docker')"></button>
</div>

Restart `docker` if needed by running this command:
<div class="code-snippet">
<pre><code>sudo systemctl restart docker</code></pre>
<button class="copy-button" onclick="copyToClipboard('sudo systemctl restart docker')"></button>
</div>

---

## Usage
Guidelines and description of the testing techniques used in this project.

The penetration testing process with `ffuf` employs a structured methodology, leveraging the `FUZZ` keyword to probe different aspects of a web application. Below is an in-depth analysis of each technique used.

Command template:
<div class="code-snippet">
<pre><code>ffuf -w [WORDLIST] -u http://SERVER_IP:PORT/FUZZ</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w [WORDLIST] -u http://SERVER_IP:PORT/FUZZ')"></button>
</div>

Note:
More advanced students can use the `SecLists` to work on more complicated vulnerabilites and learn about different types of lists used during security assessments. List types include usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells, etc. 
Each of testing techinque mentioned in this lab has a correct working command. To analyse larger outputs you can use the `wordlist.txt` list that contains much more data but it will also extend the testing process time.

In this lab we have fully working wordlists to run ffuf attacks. For each testing technique we have different wordlists:

list.txt - wordlist containing all endpoints of the vulnerable webapp (directories, subdirectories, pages)

parameters.txt - wordlist containing potential parameters 

ids.txt - wordlist containing numbers from 1 to 1000, that could be used as ID values

cookie_values.txt - wordlist containing diffferent cookie values

tokens.txt - wordlist containing token values for custom HTTP header-based authentication mechanisms

custom_header.txt - wordlist containing values for a custom header

request.txt - file containing a HTTP request

wrong_request.txt - file containing a HTTP requests with a wrong key value to test

wrong_requestv2.txt - file containing a HTTP requests with a wrong custom header

wordlist.txt - wordlist containing a lot of different data for more advanced testing

It's not recommended to modify the wordlists. They are created specifically to test this Vulnerable Web App.

TODO TODO
You can modify the `wordlist.txt` for a more indyvidualised testing purposes.

---

### Directory Fuzzing
This technique tests for directory names, seeking to uncover unsecured folders that could contain sensitive information. `FUZZ` acts as a placeholder for directory names within the URL path, and each entry from list.txt replaces `FUZZ` to test different directory combinations.

Correct command:
<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ')"></button>
</div>

Response code/Status `301`: All listed paths (about, config, admin, api) are redirecting to another location. This might indicate that these directories exist but are set up to redirect users elsewhere

This output is useful for understanding which paths exist on the server and how the server responds to requests to these paths. In penetration testing, this information is critical for mapping the application and identifying potential areas for deeper investigation.
 
---

### Page Fuzzing
Page fuzzing focuses on discovering accessible PHP files. The .php extension is fixed, and FUZZ iterates through potential file names. This could expose scripts that are unprotected or provide more information on the server's structure.

Correct command:
<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ.php')"></button>
</div>

Focuses on discovering accessible PHP files by iterating through potential file names with the `.php` extension.
index [Status: 200, ...]:  file `index.php` exists and is accessible, size, word count, and line count give an idea of the content’s complexity.

header_auth [Status: 401, ...]: Access to `header_auth.php` is unauthorized, suggesting it requires authentication, which can be a point of interest for testing authentication mechanisms.

user session.php [Status: 302, ...]: A temporary redirect response from `user_session.php`. This could indicate a redirection to a login page or another part of the application.

---

### Directory and Page Fuzzing with Extensions
Here, the `-e` flag extends the fuzzing to include file extensions, effectively searching for files of a particular type. The `-v `flag provides verbose output, offering full URLs and redirection paths, which aids in detailed analysis of the application's response.

Correct command:
<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -e .php</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -e .php')"></button>
</div>

Correct command with verbose output:
<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -e .php -v</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -e .php -v')"></button>
</div>

---

### Recursive Fuzzing
Recursive fuzzing delves into directories found during the initial fuzzing. The -recursion-depth flag determines how many levels deep ffuf will go. This is crucial for uncovering nested directories that could lead to deeper vulnerabilities.

Correct command with depth level 2:
<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -recursion -recursion-depth 2</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -recursion -recursion-depth 2')"></button>
</div>

Correct command with depth level 2 and other options:
<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -recursion -recursion-depth 2 -e .php</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -recursion -recursion-depth 2 -e .php')"></button>
</div>

Command to get all pages in the webapp:
<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -recursion -recursion-depth 2 -e .php,.css -v</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -recursion -recursion-depth 2 -e .php,.css -v')"></button>
</div>


Delves into directories found during initial fuzzing, with `-recursion-depth` controlling the levels of depth.

---

### Parameter Fuzzing for GET and POST Requests
Parameter fuzzing examines how the application processes query strings in `GET` requests and data payloads in POST requests. By altering the key parameter, we can identify how the application responds to various inputs. The `-mc` flag filters out all responses except those with specific status codes, such as `200`, indicating a successful hit.


#### GET Parameter fuzzing
Correct command:
<div class="code-snippet">
<pre><code>ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php?key=FUZZ</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php?key=FUZZ')"></button>
</div>

Correct command listing only response codes 200:
<div class="code-snippet">
<pre><code>ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php?key=FUZZ -mc 200</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php?key=FUZZ -mc 200')"></button>
</div>
<!-- ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php?key=FUZZ
ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php?key=FUZZ -mc 200 -->


#### POST Parameter fuzzing
Correct command:
<div class="code-snippet">
<pre><code>ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php -X POST -d 'key=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded'</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php -X POST -d 'key=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded')"></button>
</div>
<!-- ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php -X POST -d 'key=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -->

Examines the application's processing of query strings in `GET` requests and data payloads in `POST` requests. `-mc` flag is used to filter responses by status codes.

Access the `http://localhost/admin/index.php` with the proper parameter with this command:
<div class="code-snippet">
<pre><code>http://localhost/admin/index.php?key=3x@mpl3_K3yP@r@m3t3r_2O23</code></pre>
<button class="copy-button" onclick="copyToClipboard('http://localhost/admin/index.php?key=3x@mpl3_K3yP@r@m3t3r_2O23')"></button>
</div>

---

### Value Fuzzing
Value fuzzing tests for valid identifiers or keys. It can reveal the correct handling of expected data and expose how the application responds to valid versus invalid data. The `-mc 200` flag is used to filter responses and list only the correct IDs or keys that return a successful HTTP status.

Correct command to list the specific ID:
<div class="code-snippet">
<pre><code>ffuf -w ids.txt:FUZZ -u http://localhost/admin/flagvalue.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -mc 200</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w ids.txt:FUZZ -u http://localhost/admin/flagvalue.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -mc 200')"></button>
</div>
<!-- ffuf -w ids.txt:FUZZ -u http://localhost/admin/flagvalue.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -mc 200 -->


Command to list all IDs:
<div class="code-snippet">
<pre><code>ffuf -w ids.txt:FUZZ -u http://localhost/admin/flagvalue.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded'</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w ids.txt:FUZZ -u http://localhost/admin/flagvalue.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded')"></button>
</div>
<!-- ffuf -w ids.txt:FUZZ -u http://localhost/admin/flagvalue.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -->

Check the hidden data using this `curl` command:
<div class="code-snippet">
<pre><code>curl -X POST http://localhost/admin/flagvalue.php -H 'Content-Type: application/x-www-form-urlencoded' -d 'id=42'</code></pre>
<button class="copy-button" onclick="copyToClipboard('curl -X POST http://localhost/admin/flagvalue.php -H 'Content-Type: application/x-www-form-urlencoded' -d 'id=42'')"></button>
</div>

---

### Cookie Fuzzing
Cookie Injection Vulnerability Testing explores an application's response to manipulated cookie values. This method uncovers how the application behaves when presented with both legitimate and illegitimate cookie data. Using FFUF, we systematically can test various cookie values, focusing on the `access_token` cookie to access a restricted page in our case study the `user_session.php`.

Correct command:
<div class="code-snippet">
<pre><code>ffuf -w cookie_values.txt -u http://localhost/user_session.php -H "Cookie: access_token=FUZZ" -v</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w cookie_values.txt -u http://localhost/user_session.php -H "Cookie: access_token=FUZZ" -v')"></button>
</div>


Check the response header with this `curl` command:
<div class="code-snippet">
<pre><code>curl -b "access_token=XJ92n%23k%403ZQ%218hT6v" http://localhost/user_session.php -v</code></pre>
<button class="copy-button" onclick="copyToClipboard('curl -b "access_token=XJ92n%23k%403ZQ%218hT6v" http://localhost/user_session.php -v')"></button>
</div>

---

### Token Fuzzing
Tests the security of custom HTTP header-based authentication mechanisms. By manipulating the header values using the option `-H "X-Custom-Auth: FUZZ"` we can inject different values from the wordlist into the `X-Custom-Auth` header. The `FUZZ` keyword is a placeholder that ffuf replaces with each line from `tokens.txt`, it assesses the application's response to both legitimate and illegitimate authentication attempts. Utilizing ffuf with the `-H` flag, various potential authentication tokens are tested. This methodology is effective in pinpointing weaknesses in the implementation of header-based authentication in web applications.

Correct command:
<div class="code-snippet">
<pre><code>ffuf -w tokens.txt -u http://localhost/header_auth.php -H "X-Custom-Auth: FUZZ"</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w tokens.txt -u http://localhost/header_auth.php -H "X-Custom-Auth: FUZZ"')"></button>
</div>

Check the hidden data using this `curl` command:
<div class="code-snippet">
<pre><code>curl -H "X-Custom-Auth: 4b82Km29Fv6zQ3xT8pW5Jr7Hn" http://localhost/header_auth.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('curl -H "X-Custom-Auth: 4b82Km29Fv6zQ3xT8pW5Jr7Hn" http://localhost/header_auth.php')"></button>
</div>

Note: Header-based authentication using tokens is a secure and efficient method for managing user authentication in web services, particularly in RESTful APIs. This method leverages HTTP headers to transmit authentication tokens, which validate user sessions.

---

### Custom Header Fuzzing
In the attack, we are testing the web application's response to different custom headers. The custom header is specified in the request, and FFuF replaces the `FUZZ` placeholder in the header with values from the wordlist. We defined different payloads in the `request.txt` file. Each payload represents a different scenario or input to test the application's response. For example, you are testing with different custom headers and `POST` data values. The `request.txt` file contains the HTTP requests to be sent. Each request block in the file represents a different test case, including the custom header and payload. The `custom_header.txt` file contains a list of potential values that FFuF will substitute for the `FUZZ` placeholder in the custom header. FFuF will test each value from the wordlist against the custom header.

`-request request.txt` - specifies the request file that contains the HTTP requests to be sent. 

`-request test_request.txt` - specifies different request send that has the FUZZ placeholder in the key value

`-u http://localhost/custom_header.php` - specifies the base URL of the target web application.

Correct command:
<div class="code-snippet">
<pre><code>ffuf -w custom_header.txt -request request.txt -u http://localhost/custom_header.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w custom_header.txt -request request.txt -u http://localhost/custom_header.php')"></button>
</div>

Correct command with a different request:
<div class="code-snippet">
<pre><code>ffuf -w test_values.txt -request test_request.txt -u http://localhost/custom_header.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w test_values.txt -request test_request.txt -u http://localhost/custom_header.php')"></button>
</div>

Wrong command to test different output:
<div class="code-snippet">
<pre><code>ffuf -w custom_header.txt -request wrong_request.txt -u http://localhost/custom_header.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w custom_header.txt -request wrong_request.txt -u http://localhost/custom_header.php')"></button>
</div>

Wrong command to test different output:
<div class="code-snippet">
<pre><code>ffuf -w custom_header.txt -request wrong_requestv2.txt -u http://localhost/custom_header.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w custom_header.txt -request wrong_requestv2.txt -u http://localhost/custom_header.php')"></button>
</div>


Check the hidden data using this `curl` command:
<div class="code-snippet">
<pre><code>curl -X POST http://localhost/custom_header.php -H "X-Custom-Header: testheader" -H "Content-Type: application/x-www-form-urlencoded" -d "key=secretValue"</code></pre>
<button class="copy-button" onclick="copyToClipboard('curl -X POST http://localhost/custom_header.php -H "X-Custom-Header: testheader" -H "Content-Type: application/x-www-form-urlencoded" -d "key=secretValue"')"></button>
</div>

---

Each method is crafted to test for different vulnerabilities, with the placement of `FUZZ` designed to mimic attacker actions and ensure comprehensive coverage of common attack vectors.


This README provides a clear guide to using ffuf for penetration testing, including detailed code snippets for each type of fuzzing technique.

---

## Learning Scenario
**Step 1:** [Directory Fuzzing](#directory-fuzzing)

This step aims to uncover hidden or unlisted directories in the web application. These directories might contain sensitive information or administrative interfaces. Begin with discovering directories in the web application.
<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ')"></button>
</div>

Observation:

Notice directories like `config`, `rce`, `api`, and especially `admin`. The `admin` directory often contains administrative controls and sensitive functionalities of the web application. It's a critical area that could provide extensive control over the application if compromised. Unauthorized access to the `admin` panel can lead to severe security breaches, including data theft, site defacement, and complete system takeover.  Once you identify an `admin` directory, prioritize it for in-depth exploration. It's a high-value target for attackers, so understanding its security is crucial. Use specialized fuzzing techniques to uncover hidden pages or functionalities within the `admin` panel. 


**Step 2:** [Page Fuzzing](#page_fuzzing)

Fuzz for pages within directories to explore further. 

<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -e .php -v</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -e .php -v')"></button>
</div>
Observation:

After running Page FUzzing you should have found these pages: index, header, xss_vulnerable, custom_header, user_session, footer, contact, header_auth, login.
Learn More: [Directory and Page Fuzzing with Extensions](#directory-and-page-fuzzing-with-extensions)

**Step 3:** [Recursive Fuzzing](#recursive-fuzzing)

Explore all possible parts of the web application. Go beyond the first level of directories and files to explore deeper nested structures. Methodically search through nested directories. Start with broader directories and progressively drill down to more specific paths.
<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -recursion -recursion-depth 2</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -recursion -recursion-depth 2')"></button>
</div>
<div class="code-snippet">
<pre><code>ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -recursion -recursion-depth 2 -e .php</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w list.txt:FUZZ -u http://localhost/FUZZ -recursion -recursion-depth 2 -e .php')"></button>
</div>
Observation:

You should have found many direcorties, subdirectories and pages with `php` and `css` extensions. After fuzzing the admin directory, certain pages like `index.php` and `flagvalue.php` are not accessible, while `settings.php`, `/users/index.php`, and `/users/profile.php` are accessible, indicating potential vulnerabilities.

**Step 4:** Identifying Attack Vectors

Focus on vulnerable parts of the web application. Use the information gathered from previous steps to pinpoint specific areas that might be vulnerable to different types of attacks.

Hint Acquisition:
<div class="code-snippet">
<pre><code>curl http://localhost/admin/index.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('curl http://localhost/admin/index.php')"></button>
</div>
Observation:

You can see that you should use parameter fuzzing testing technique.

[Parameter Fuzzing for GET and POST Requests](#parameter-fuzzing-for-get-and-post-requests)
Apply GET and POST requests fuzzing on /admin/index.php
<div class="code-snippet">
<pre><code>ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php?key=FUZZ</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php?key=FUZZ')"></button>
</div>

<div class="code-snippet">
<pre><code>ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php -X POST -d 'key=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded'</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w parameters.txt:FUZZ -u http://localhost/admin/index.php -X POST -d 'key=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded'')"></button>
</div>


Hint Acquisition about `/admin/flagvalue.php`:
<div class="code-snippet">
<pre><code>curl http://localhost/admin/flagvalue.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('curl http://localhost/admin/flagvalue.php')"></button>
</div>
Observation:

Now you can see that we should use the [Value Fuzzing](#value-fuzzing). Use this method to gain access to `/admin/flagvalue.php` file.

Correct command to list all IDs:
<div class="code-snippet">
<pre><code>ffuf -w ids.txt:FUZZ -u http://localhost/admin/flagvalue.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded'</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w ids.txt:FUZZ -u http://localhost/admin/flagvalue.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded')"></button>
</div>


**Step 5:** Advanced Testing Endpoints
Test various accessible and inaccessible pages. Apply specialized testing techniques to different types of endpoints discovered in the application, including those that require authentication or specific headers.

In this step, focus on advanced testing techniques for various web pages, including those that are both accessible and inaccessible. This process helps identify potential vulnerabilities in different parts of the web application.

Objective:

The goal is to understand how different endpoints react to various testing methods and to identify security flaws or misconfigurations in the application.

Accessible Pages:

Start with pages like `xss_vulnerable.php`, /`rce/remote_code_execution.php`. These pages might be vulnerable to specific attacks like Cross-Site Scripting (XSS) or Remote Code Execution (RCE).

Action:
Try different input values in these pages URL parameters or forms to see how the application responds. Look for indications of script execution or unexpected behaviors.

Inaccessible Pages:

Focus on pages like `user_sessions.php`, `header_auth.php`, and `custom_header.php`. These pages are not directly accessible, indicating they might require specific authentication or headers.

Hint Acquisition:
Initially, use the curl command to explore HTTP responses:
<div class="code-snippet">
<pre><code>curl http://localhost/user_session.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('curl http://localhost/user_session.php')"></button>
</div>

Observations:

Note down the response headers, status codes, and any error messages. These details can give clues about the required authentication mechanism or other access controls.

[Cookie Fuzzing](#cookie-fuzzing):

This method targets how the application handles cookies, which are often used for session management.

Testing `user_session.php`:
<div class="code-snippet">
<pre><code>ffuf -w cookie_values.txt -u http://localhost/user_session.php -H "Cookie: access_token=FUZZ" -v</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w cookie_values.txt -u http://localhost/user_session.php -H "Cookie: access_token=FUZZ" -v')"></button>
</div>

Using curl to Test Valid Session Tokens:
<div class="code-snippet">
<pre><code>curl -b "access_token=XJ92n%23k%403ZQ%218hT6v" http://localhost/user_session.php -v</code></pre>
<button class="copy-button" onclick="copyToClipboard('curl -b "access_token=XJ92n%23k%403ZQ%218hT6v" http://localhost/user_session.php -v')"></button>
</div>

Learning Outcome:

Understand how the application validates session cookies and identify any weaknesses in session management.

[Token Fuzzing](#token-fuzzing):

Focuses on how the application validates custom authentication tokens.

Targeting `header_auth.php`:
<div class="code-snippet">
<pre><code>ffuf -w tokens.txt -u http://localhost/header_auth.php -H "X-Custom-Auth: FUZZ"</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w tokens.txt -u http://localhost/header_auth.php -H "X-Custom-Auth: FUZZ"')"></button>
</div>

Direct Testing with curl:
<div class="code-snippet">
<pre><code>curl -H "X-Custom-Auth: 4b82Km29Fv6zQ3xT8pW5Jr7Hn" http://localhost/header_auth.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('curl -H "X-Custom-Auth: 4b82Km29Fv6zQ3xT8pW5Jr7Hn" http://localhost/header_auth.php')"></button>
</div>
Learning Outcome:

Identify if the custom tokens are validated securely and if there are ways to bypass this authentication.

[Custom Header Fuzzing](#custom-header-fuzzing):

Understanding the Custom Header Method:

Custom headers, like `X-Custom-Header`, are often used by web applications for various purposes, including authentication, feature control, or internal tracking. Manipulating these headers can reveal how the server processes them, potentially uncovering security flaws. The wordlist `custom_header.txt` will contain various values that ffuf will inject in place of FUZZ in the `X-Custom-Header`. The goal is to try different header values to see how the server responds, looking for anything out of the ordinary that could indicate a vulnerability. Ensure your wordlist `custom_header.txt` includes a variety of header values. These could be common tokens, known patterns, or even unexpected or malformed inputs. Example values might include standard tokens, random strings, or special characters. The request file defines the HTTP request format. `FUZZ` will be replaced by each entry in your wordlist. `POST /custom_header.php HTTP/1.1` initiates a `POST` request to `custom_header.php`. `Content-Length: 13` indicates the length of the body. If you change the body content, adjust this value accordingly.

Analyzing Responses:
Monitor how the server responds to each modified header. Look for changes in status codes, error messages, or any other output that differs from the norm. A successful fuzz might show an unintended server behavior, error messages revealing server info, or even a full response indicating a successful exploitation.

Tests the application's handling of non-standard HTTP headers.
Commands for `custom_header.php`:
<div class="code-snippet">
<pre><code>ffuf -w custom_header.txt -request request.txt -u http://localhost/custom_header.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w custom_header.txt -request request.txt -u http://localhost/custom_header.php')"></button>
</div>
<div class="code-snippet">
<pre><code>ffuf -w test_values.txt -request test_request.txt -u http://localhost/custom_header.php</code></pre>
<button class="copy-button" onclick="copyToClipboard('ffuf -w test_values.txt -request test_request.txt -u http://localhost/custom_header.php')"></button>
</div>

Curl Command for Direct Access:
<div class="code-snippet">
<pre><code>curl -X POST http://localhost/custom_header.php -H "X-Custom-Header: testheader" -H "Content-Type: application/x-www-form-urlencoded" -d "key=secretValue"</code></pre>
<button class="copy-button" onclick="copyToClipboard('curl -X POST http://localhost/custom_header.php -H "X-Custom-Header: testheader" -H "Content-Type: application/x-www-form-urlencoded" -d "key=secretValue"')"></button>
</div>
Learning Outcome:

Gain insights into how custom headers are processed and if they can be exploited. By using a correct payload you should gain access to the `custom_header.php` page.

## License
License information for the project. For learning puproses only.


<!-- <div class="code-snippet">
<pre><code></code></pre>
<button class="copy-button" onclick="copyToClipboard('')"></button>
</div> -->