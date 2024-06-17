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

In today's interconnected world, ensuring data security is paramount. Online communications demand robust protection against eavesdropping and breaches of confidentiality. SSL/TLS (Secure Sockets Layer / Transport Layer Security) protocols and their derivatives, such as mTLS (mutual TLS), play a pivotal role in upholding security standards by providing authentication, confidentiality, and data integrity.

This project focuses on an automated certificate generation service powered by Ansible playbooks. The primary objective is to streamline the creation of SSL/TLS certificates based on a structured architecture defined within a YAML file.

## SSL/TLS/mTLS Context and Challenges

SSL/TLS serves as a fundamental protocol for securing online communications by encrypting data and ensuring server authenticity. Digital certificates play a vital role in authenticating parties communicating online. The deployment of digital certificates is crucial in modern information security, particularly in financial transactions, government communications, and everyday online interactions.

TLS certification presents several challenges:

* Confidentiality: Protecting sensitive data by encrypting it to prevent malicious interceptions.
* Authentication: Verifying the identity of parties communicating online to prevent "Man-in-the-Middle" attacks.
* Integrity: Ensuring data exchanged between parties remains unaltered during transit.
* Server Security: Shielding servers from attacks by validating client identities.
* Access Control: Restricting access to online resources to authorized users only.

## The SSL Certification Service

This tool, leveraging Ansible, offers a comprehensive solution for creating and managing TLS certification architectures, effectively addressing the aforementioned security challenges. Operating from a YAML input file and an Ansible playbook, our tool encompasses the following key features:

* Root Authority Creation: Capability to create Root Authorities, establishing the highest level of trust.
* Intermediate Certificates: Generation of intermediate certificates with the ability to validate others.
* Cascade Signing: Signing multiple intermediate certificates with a single Root Authority.
* Output Products: Generation of essential output products for certificate management, including certificates in PEM format, keys, Certificate Signing Request (CSR), bundles, and CA chains.

* **Note: If the same certificate is requested multiple times, the service will revoke the previous one and create a new one upon request. Previous CAs are retained between launches, but not CERTs.**

## Getting Started

### Prerequisites

To use this tool, you'll need:

* Ansible installed on your system.
* A YAML input file with the desired certification architecture configuration (default is pki/CA_NAME/input.yml).
* A root access / sudoer account.

### Usage

* Clone this repository to your local machine.
* Navigate to the project directory.
* Edit the .gpg.key file to generate a key for certificate encryption.
* Edit the .vault.key file to generate a key for Ansible input encryption.
* Edit the .nexus.env file and fill in your Nexus/Artifactory information.
* Edit the .env file with your desired values (output folder, binary files, etc.).
* Replace or remove the ./pki/EXAMPLES folder and create your CA architecture.
* Initially generate your CA (only if you prefer not to redeploy all your CA each time).
* Customize the .gitlab-ci.yml file to build your certification service based on CA names.
* This project includes a pre-commit script to encrypt your content (Ansible input files, CAs, private keys) using GPG. Scripts in ./bin allow for decryption/encryption at any time. You can locally push changes to your remotes using the ./bin/push_ca script.

The Ansible playbook relies on all vars in default/examples. Ensure a non-empty list of CA and CERTs for correct playbook execution. Store CA key passwords inside the input folder, hence everything is encrypted.

Organizing CAs and sub-CAs in separate folders, as currently structured, improves readability and prevents lengthy YAML files.

To expedite certification as a service, add CICD vars in your pipeline:

```SHELL
${CICD_GPG_KEY} # GPG decryption of CA and CERTS private data
${CICD_ANSIBLE_VAULT_KEY} # Ansible input decryption
#
${NEXUS_REPOSITORY_URL} # Your remote address
${NEXUS_REPOSITORY_NAME} # Your remote repository name/path
${NEXUS_REPOSITORY_URL} # Concatened value for pushing
${GITLAB_CI_NEXUS_CREDENTIALS_USR} # User for push operations
${GITLAB_CI_NEXUS_CREDENTIALS_PSW} # User password
```

Masking vars in this manner facilitates their modification. More informations inside the GitLab CI file.

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-07-26: First Init

* First init of this playbook with the bootstrap_playbook playbook by Lord Robin Crombez
* Added bin/certification scrip to build custom SSL certification layers

### 2023-12-08: CI and SSL as service

* This project retains or creates all your data/certs.
* Allows creation and push of certs to a Nexus/Artifactory repository.
* Handles revocation and rewriting.
* CICD Push certs.

### 2023-12-19: Cert push fix and pre-commit script

* Added pre-commit script in ./bin (dont forget to install in your .git/hooks and chmod +x)
* Fix the push script: certs wanst pushed

### 2023-12-19

* Changed vars and change CICD for better performances
* Added SonarQube for quality checks
* CICD contains now a "publish" stage, GitLab Release will be create on "main", and certificates will be publish on "main" to, based on timestamp
* You can edit the CICD to change the publish output and set "latest" version for crypto material
* CICD push to a private remote Nexus, so ${VERSION-TIMESTAMP} is used for identification

### 2024-06-17: Reworks and automation

* Repos now use custom genetation to create certification pipeline
* Added detect secret to the CI
* Added Mardown/YAML/Ansible/secret steps to the pipeline
* Fixed and edited vars to follow new guidelines
* Fix bundles and ZIP content to the crypt process

## Authors

* Lord Robin Crombez

## Sources

* [Ansible playbook documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_playbooks.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
