# SSL-Certification-As-Service

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Cbz-blue)

## Description

![Tag: Ansible](https://img.shields.io/badge/Tech-Ansible-orange)
![Tag: Debian 10-11](https://img.shields.io/badge/Tech-Debian%2010--11-orange)
![Tag: Automation](https://img.shields.io/badge/Tech-Automation-orange)
![Tag: SSL-TLS-mTLS](https://img.shields.io/badge/Tech-SSL--TLS--mTLS-orange)

## Introduction

In an increasingly interconnected world, data security is paramount. Online communications must be protected against eavesdropping and breaches of confidentiality. SSL/TLS (Secure Sockets Layer / Transport Layer Security) protocols and their derivatives, such as mTLS (mutual TLS), play a crucial role in ensuring security by providing authentication, confidentiality, and data integrity.

## SSL/TLS/mTLS Context and Challenges:

SSL/TLS is a protocol for securing online communications by encrypting data and ensuring the authenticity of servers. Authentication is accomplished through digital certificates, which establish trust between parties communicating online. In the context of modern information security, the deployment of digital certificates is essential to safeguard sensitive data, particularly in financial transactions, government communications, and everyday online interactions.

The challenges of TLS certification are numerous, including:

1. **Confidentiality:** Protecting sensitive data against malicious interceptions by encrypting it.
2. **Authentication:** Verifying the identity of parties communicating online, thereby preventing "Man-in-the-Middle" attacks.
3. **Integrity:** Ensuring that exchanged data is not altered in transit.
4. **Server Security:** Shielding servers from attacks by verifying client identities.
5. **Access Control:** Restricting access to online resources to authorized users only.

## The SSL Certification Service

This tool, based on Ansible, provides a comprehensive solution for creating and managing TLS certification architectures, addressing the security challenges mentioned above. It operates from a YAML input file and an Ansible playbook. Here are the main features of our tool:

- **Root Authority Creation:** You can create Root Authorities to establish the highest level of trust.
- **Intermediate Certificates:** Our tool allows you to generate intermediate certificates that can validate others.
- **Cascade Signing:** It's possible to sign multiple intermediate certificates with a single Root Authority.
- **Output Products:** The tool generates various essential output products for certificate management, including certificates in PEM format, keys, Certificate Signing Request (CSR), bundles, and CA chains.

If you ask for the same certificate more thant 1 time, the service will revoke the previous one and create another one, as you asked. So previous CERTs and CAs are keeped between 2 launch.

By default, ./Ansible and ./Certifications are ignored by Git. You can remove this and commit your certs into your repository, so automated deployments can remotly access to your repository. If you are note on premise, I deffinatly NOT advise you to do it.

## Getting Started

### Prerequisites

To use this tool, you'll need:

- Ansible installed on your system.
- A YAML input file with the desired certification architecture configuration (default is bin/input.yml).
- A root access / sudoer account.

### Usage

1. Clone this repository to your local machine.
2. Navigate to the project directory.
3. Edit bin/input.yml and define your desired output.
4. Execute the bin/certifications script.
5. Get your content in the setted directory (default is ./Certifications)

Example:

```bash
cd ./bin
chmod +x ./certifications
sudo ./certifications
```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-07-26: First Init

* First init of this playbook with the bootstrap_playbook playbook by Lord Robin Crombez
* Added bin/certification scrip to build custom SSL certification layers

## Authors

* Lord Robin Crombez

## Sources

* [Ansible playbook documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_playbooks.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
