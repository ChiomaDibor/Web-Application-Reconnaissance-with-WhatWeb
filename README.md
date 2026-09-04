# Web Application Reconnaissance with WhatWeb

## Overview

This project demonstrates web application reconnaissance and technology fingerprinting using WhatWeb against a Metasploitable 2 virtual machine in an isolated laboratory environment.

The objective was to identify technologies exposed by the target web server, including the web server software, operating system, server-side technologies, versions, HTTP headers, and WebDAV configuration.

## Objectives

* Identify the target web server.
* Identify the underlying operating system.
* Identify server-side technologies.
* Identify software versions exposed by the web server.
* Inspect HTTP response headers.
* Perform web technology fingerprinting using WhatWeb.
* Document and analyse the reconnaissance findings.

## Lab Environment

| Component      | Details           |
| -------------- | ----------------- |
| Assessment VM  | Kali Linux        |
| Target VM      | Metasploitable 2  |
| Tool           | WhatWeb           |
| Virtualization | Oracle VirtualBox |
| Network        | Host-Only Network |
| Target IP      | `192.168.56.101`  |

## Methodology

The assessment followed these steps:

1. Identified the IP address of the Metasploitable 2 target.
2. Verified connectivity between Kali Linux and the target.
3. Inspected the target's HTTP response headers using cURL.
4. Performed web technology fingerprinting using WhatWeb.
5. Saved the WhatWeb output for documentation.
6. Analysed the identified technologies and security implications.

## Commands Used

### Identify network configuration

```bash
ifconfig
```

### Test connectivity

```bash
ping -c 4 192.168.56.101
```

### Inspect HTTP headers

```bash
curl -I http://192.168.56.101
```

### Perform WhatWeb fingerprinting

```bash
whatweb -v http://192.168.56.101
```

### Save WhatWeb results

```bash
whatweb -v http://192.168.56.101 | tee whatweb-results.txt
```

## Key Findings

The reconnaissance identified the following technologies:

| Technology             | Finding                   |
| ---------------------- | ------------------------- |
| Web Server             | Apache HTTP Server        |
| Apache Version         | 2.2.8                     |
| Operating System       | Ubuntu Linux              |
| Server-Side Technology | PHP                       |
| PHP Version            | 5.2.4-2ubuntu5.10         |
| WebDAV                 | DAV/2                     |
| HTTP Status            | 200 OK                    |
| Page Title             | Metasploitable2 - Linux   |
| CMS                    | Not identified by WhatWeb |
| JavaScript Library     | Not identified by WhatWeb |

The HTTP response also exposed the following headers:

```text
Server: Apache/2.2.8 (Ubuntu) DAV/2
X-Powered-By: PHP/5.2.4-2ubuntu5.10
```

These headers provide useful information about the underlying technology stack and demonstrate the value of reconnaissance and technology fingerprinting.

## Screenshots

The `screenshots/` directory contains evidence collected during the laboratory exercise, including:

* Target IP configuration
* Successful connectivity test
* HTTP header inspection
* WhatWeb scan results
* Detailed technology findings

## Results

The raw WhatWeb output is available in:

`results/whatweb-results.txt`

## Report

The complete Proof of Concept report is available in:

`report/WhatWeb-Web-Application-Reconnaissance.pdf`

## Security Considerations

The exercise identified legacy software versions and technology information exposed through HTTP headers.

Potential security considerations include:

* Review and update legacy web server and PHP versions.
* Minimize unnecessary technology and version disclosure.
* Review whether WebDAV is required.
* Disable unnecessary services and functionality.
* Maintain an accurate technology inventory.
* Conduct regular vulnerability assessments.

The identified technologies do not by themselves prove that a vulnerability exists. Further security testing would be required to validate specific vulnerabilities.

## Disclaimer

This project was conducted exclusively in an authorized, isolated laboratory environment using Metasploitable 2, a deliberately vulnerable virtual machine designed for cybersecurity education and testing.

The techniques demonstrated should only be used against systems for which explicit authorization has been obtained.
