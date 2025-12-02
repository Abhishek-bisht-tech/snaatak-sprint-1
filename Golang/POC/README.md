## POC:Golang CI checks with DAST (OWASP ZAP Baseline Scan)


  <img src="https://github.com/user-attachments/assets/7d273bcc-b6e4-4f6a-aa21-5ac83c53648b" alt="OWASP ZAP Workflow Diagram" width="400"/>
</p>


---

## **Author Table**

| **Field**   | **Author Name** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ----------- | --------------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | -------------------------- |
| **Details** | Abhishek        | 26-11-2025     | 1.0         | Abhishek            | 26-11-2025         |                  |                 |                 |                            |


---

# **Table of Contents**

- [Introduction](#introduction)
- [Pre-requisites](#pre-requisites)
- [Clone the Repository](#clone-the-repository)
- [Run Employee API with Docker](#run-employee-api-with-docker)
- [Verify API is Running Swagger UI](#verify-api-is-running-swagger-ui)
- [Pull OWASP ZAP Docker Image](#pull-owasp-zap-docker-image)
- [Run OWASP ZAP Baseline Scan Against Employee API](#run-owasp-zap-baseline-scan-against-employee-api)
- [ZAP Scan Output JSON](#zap-scan-output-json)
- [ZAP HTML Report](#zap-html-report)
- [Key Findings](#key-findings)
  - [High Severity](#high-severity)
  - [Medium Severity](#medium-severity)
  - [Low Severity](#low-severity)
  - [Informational](#informational)
- [Conclusion](#10-conclusion)
- [Contact](#contact)
- [References](#references)


---

## **Introduction**

This document explains the step-by-step process of running the *employee-api* locally using Docker and performing a Dynamic Application Security Test (DAST) using **OWASP ZAP** (ZAP Baseline Scan). All steps are supported with the screenshots captured during execution.

---

## **Pre-requisites**

| Tool / Requirement | Purpose                   | Command to Verify  |
| ------------------ | ------------------------- | ------------------ |
| Go (1.20+)         | Run the Employee-API      | `go version`       |
| Docker Engine      | Required to run OWASP ZAP | `docker --version` |
| curl               | Test API endpoints        | `curl --version`   |
| jq (optional)      | Pretty-print JSON reports | `jq --version`     |
| Git                | Clone the repository      | `git --version`    |

---

## **Clone the Repository**

Clone the employee-api repository locally:

```bash
git clone https://github.com/OT-MICROSERVICES/employee-api
cd employee-api
```

---

## **Run Employee API with Docker**

Build and run the employee API container:

```bash
docker build -t employee-api .
docker run -p 8080:8080 employee-api
```

The API starts successfully and exposes all routes including Swagger UI.

<img width="1491" height="411" alt="Screenshot from 2025-12-02 11-15-34" src="https://github.com/user-attachments/assets/d127fca7-a409-4bf9-8a9d-6ef430a2d335" />


---

## **Verify API is Running (Swagger UI)**

Open browser:

```
http://localhost:8080/swagger/index.html
```

Swagger UI loads showing all available API endpoints.

<img width="1846" height="1014" alt="Screenshot from 2025-12-02 12-24-23" src="https://github.com/user-attachments/assets/bfb57d78-fd42-453f-ab46-278732ccb105" />


---

## **Pull OWASP ZAP Docker Image**

```bash
docker pull ghcr.io/zaproxy/zaproxy:latest
```
<img width="1854" height="588" alt="Screenshot from 2025-12-01 09-29-48" src="https://github.com/user-attachments/assets/4b5f2b67-2fed-40ac-b7b9-ecea3e39260e" />


---

## **Run OWASP ZAP Baseline Scan Against Employee API**

Run ZAP baseline scan with target URL:

```bash
docker run --rm \
  --network host \
  -v "$(pwd)/zap:/zap/wrk" \
  ghcr.io/zaproxy/zaproxy:latest \
  zap-baseline.py \
  -t http://localhost:8080/swagger/index.html \
  -r zap_report.html \
  -J zap_report.json
```

This command:

* Uses host networking to reach local API
* Saves HTML & JSON reports inside `zap` folder

<img width="1846" height="1014" alt="Screenshot from 2025-12-02 12-26-57" src="https://github.com/user-attachments/assets/0373a5f9-cc53-4e8a-bdd2-e5cf649d6def" />

---

## **ZAP Scan Output (JSON)**

ZAP produced `zap_report.json` containing all detected alerts.
You can view it using:

```bash
jq . zap_report.json
```
<img width="1846" height="982" alt="Screenshot from 2025-12-02 12-36-38" src="https://github.com/user-attachments/assets/84e478e8-674c-481a-a46c-b5cb5678734f" />


---

## **ZAP HTML Report**

The HTML report `zap_report.html` shows:

* 1 High severity alert
* 2 Medium
* 4 Low
* 3 Informational

<img width="1846" height="1047" alt="Screenshot from 2025-12-02 12-28-26" src="https://github.com/user-attachments/assets/f847c1fe-cddd-4964-8705-341e2ab64259" />


---

## **Key Findings**

ZAP detected the following major issues:

### **High Severity**

* **Vulnerable JS Library** — DOMPurify v2.3.10 (CVE references visible)

### **Medium Severity**

* Missing CSP header
* Missing Anti-clickjacking header

### **Low Severity**

* Content-Type header missing
* Sensitive comments
* Permissions policy missing

### **Informational**

* Storage & cacheable content
* Suspicious comments



---

## **10. Conclusion**

The PoC demonstrates:

* Successful deployment of Employee API using Docker
* Execution of an automated OWASP ZAP DAST scan
* Generation of both HTML & JSON vulnerability reports

These findings help assess security posture and indicate areas to apply security headers, dependency upgrades, and code fixes.


---


## **Contact**


| **Field**  | **Details**                                                                           |
| ---------- | ------------------------------------------------------------------------------------- |
| **Author** | Abhishek                                                                              |
| **Email**  | [abhishek.bisht.snaatak@mygurukulam.co](mailto:abhishek.bisht.snaatak@mygurukulam.co) |



## **References**

| Link                                                                                                 | Description                             |
| ---------------------------------------------------------------------------------------------------- | --------------------------------------- |
| [https://www.zaproxy.org](https://www.zaproxy.org)                                                   | Official OWASP ZAP Documentation        |
| [https://github.com/zaproxy/action-baseline](https://github.com/zaproxy/action-baseline)             | GitHub Action for ZAP Baseline Scan     |
| [https://www.opentext.com/what-is/dast](https://www.opentext.com/what-is/dast)                       | DAST Overview                           |
| [https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)                     | OWASP Top 10                            |
| [https://github.com/OT-MICROSERVICES/employee-api](https://github.com/OT-MICROSERVICES/employee-api) | Employee-API Repository (If applicable) |
