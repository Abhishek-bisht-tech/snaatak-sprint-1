# GoLang CI Checks - DAST 

  <img src="https://github.com/user-attachments/assets/7d273bcc-b6e4-4f6a-aa21-5ac83c53648b" alt="OWASP ZAP Workflow Diagram" width="400"/>
</p>

## Author table

| **Field**   | **Author Name** | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer (Optional)** |
| ----------- | --------------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | -------------------------- |
| **Details** | Abhishek        | 28-11-2025     | 1.0         | Abhishek            | 28-11-2025         |                  |                 |                 |                            |

---

## Table of Contents
- [Introduction](#introduction)
- [What is Application CI?](#what-is-application-ci)
- [Why CI is Important](#why-ci-is-important)
- [GoLang CI Checks](#golang-ci-checks)
- [What is DAST?](#what-is-dast)
- [Combined Workflow Diagram](#combined-workflow-diagram)
- [Tools Comparison](#tools-comparison)
- [Advantages](#advantages)
- [Proof of Concept (POC)](#proof-of-concept-poc)
- [Best Practices](#best-practices)
- [Recommendation / Conclusion](#recommendation--conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---

## Introduction
This documentation provides a comprehensive overview of Application CI Design, GoLang Continuous Integration (CI) Checks, and Dynamic Application Security Testing (DAST). It explains the core concepts, benefits, workflows, tools, comparisons, best practices, and a POC approach that teams can implement to strengthen build pipelines and security posture.

---

## What is Application CI?
**Continuous Integration (CI)** is a practice where developers frequently merge code changes into a shared repository. Each merge triggers an automated pipeline that includes build, test, quality checks, and security validations.

### Key Objectives:
- Automate build and test processes  
- Ensure code quality and consistency  
- Reduce integration issues  
- Detect bugs early through automated testing  

---

## Why CI is Important
- Enables faster development cycles  
- Minimizes integration conflicts  
- Ensures immediate feedback to developers  
- Improves product reliability  
- Reduces manual effort across build and test phases  

---

## GoLang CI Checks
GoLang CI Checks help identify code quality issues, formatting inconsistencies, security vulnerabilities, and potential runtime errors.

### Common GoLang CI Tools
| Tool | Purpose |
|------|---------|
| **golangci-lint** | Linting, static analysis |
| **go vet** | Detect suspicious constructs |
| **go test** | Run unit tests and benchmarks |
| **gosec** | Security scanning |
| **govulncheck** | Detects vulnerable dependencies |
| **SonarQube for Go** | Code quality & security analysis |

### GoLang CI Workflow
1. Checkout code from repository  
2. Install dependencies  
3. Run format & lint checks  
4. Run static analysis (go vet / gosec)  
5. Run unit tests with coverage  
6. Generate reports  
7. Publish artifacts & quality gates  

---

## What is DAST?
**Dynamic Application Security Testing (DAST)** analyzes a running application to detect security vulnerabilities such as SQL injection, XSS, CSRF, authentication weaknesses, and insecure server configurations.

### DAST focuses on:
- Runtime behavior  
- External attack surface  
- Vulnerabilities exploitable by attackers  

### Popular DAST Tools
| Tool | Description |
|------|-------------|
| **OWASP ZAP** | Open-source scanner for web apps |
| **Burp Suite** | Widely-used DAST tool for manual/automated security testing |
| **Acunetix** | Enterprise-grade security scanner |
| **Netsparker** | Automated web vulnerability scanner |

---

## Combined Workflow Diagram

![bd1dd148-59f5-40e3-b8f5-b77aeec0dfa7](https://github.com/user-attachments/assets/ad89473a-05b6-41dc-80d0-433e180c00a6)


## Tools Comparison

| Category        | Tool           | Pros                                | Cons                        |
| --------------- | -------------- | ----------------------------------- | --------------------------- |
| Linting         | golangci-lint  | Fast, multi-linter, configurable    | Can be strict for beginners |
| Static Security | gosec          | Detects real Go security issues     | Sometimes false positives   |
| DAST            | OWASP ZAP      | Free, automated, supports API scans | Slower vs paid tools        |
| DAST            | Burp Suite Pro | Very powerful & reliable            | Paid license                |
| Quality         | SonarQube      | Holistic quality gates              | Requires server setup       |

---

## Advantages of CI + GoLang Checks + DAST

- Catches code issues early
- Reduces security risk before production
- Ensures consistent build quality
- Automates developer workflows
- Improves team efficiency & reliability
- Meets compliance and audit requirements

## Best Practices

### **CI**
- Keep pipelines fast and efficient  
- Use caching to reduce build time  
- Enable branch protection rules  

### **GoLang Code Quality**
- Enforce `golangci-lint`  
- Maintain test coverage ≥ **70%**  
- Scan dependencies regularly  

### **Security & DAST**
- Configure scheduled DAST scans  
- Validate all CI reports before merging  
- Integrate **SAST + DAST** for complete coverage  
- Review false positives manually  


---

## Recommendation / Conclusion

A well-structured CI pipeline with GoLang quality checks and integrated DAST improves:

- **Code reliability**  
- **Deployment confidence**  
- **Application security posture**

This approach is highly recommended for DevOps teams building **secure and scalable GoLang applications**.


---

## Contact Information

| Contact Type | Details |
|--------------|---------|
| Email | abhishek.bisht.snaatak@mygurukulam.co |


---

## References

| Reference | Link |
|----------|------|
| Go Documentation | https://go.dev/doc/ |
| golangci-lint | https://golangci-lint.run/ |
| OWASP ZAP | https://www.zaproxy.org/ |
| GitHub Actions Documentation | https://docs.github.com/actions |

---
