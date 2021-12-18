Title: PCI Secure Software Standard
Date: 2021-12-17 11:50:00
Category: 
Tags: PCI, Infosec
Slug: 
Summary: PCI Secure Software Standard
Status: draft



### Secure Software Standard
![SSS Overview](/images/pci-ssf/2.png)

* **Part of the PCI Software Security Framework**
 * Provides security requirements for building secure payment software to protect the integrity and the confidentiality of sensitive data that is stored, processed, or transmitted in association with payment transactions. 
 * Provide assurance that payment software is designed, engineered, developed, and maintained in a manner that protects payment transactions and data, minimizes vulnerabilities, and defends itself from attacks.
 * Intended for vendors that develop payment software that supports or facilitates payment transactions

## Requirements
* Processes used by the software vendor to identify and support software security controls.
* Coverage of all payment software functionality, including but not limited to:
    * End-to-end payment functionality,
    * Inputs and outputs,
    * Handling of error conditions,
    * Interfaces and connections to other files, systems, and/or software or software components,
    * All data flows, and
    * All security mechanisms, controls, and countermeasures (e.g., authentication, authorization, validation, parameterization,
    segmentation, logging, etc.).
* Coverage of guidance the software vendor is expected to provide to its customers to ensure:
    * Customers are aware how to implement and operate the payment software securely;
    * Customers are provided guidance on configuration options of the execution environment and system components;
    * Customers are provided guidance on how to implement security updates; and
    * Customers and other stakeholders are aware how and where to report security issues.
* Note that the software vendor may be expected to provide such guidance even when the specific setting:
    * Cannot be controlled by the payment software once the software is installed by the customer; or
    * Is the responsibility of the customer and not the software vendor.
* Coverage of all supported platforms and execution environments for the payment software.
* Coverage of all tools (reporting tools, logging tools, etc.) and functions (e.g., system calls or APIs) used by or within the payment software
to access critical assets.
* Coverage of all payment software components and dependencies, including supported execution platforms or environments, third-party
and open-source libraries, services, and other required functions.
* Coverage of any other types of software necessary for a full implementation of the payment software.


### Spec
[SSS Spec](https://www.pcisecuritystandards.org/documents/PCI-Secure-Software-Standard-v1_1.pdf)

