# Security and Confidentiality

## Overview

The Desk Reservation Attendance System was developed within a real organizational environment. As a result, special care has been taken to ensure that sensitive information is not exposed in this public repository.

This document outlines how security, privacy, and confidentiality were handled both in the system design and in the materials shared publicly.

---

## Core Principles

The system follows these key principles:

- **Data Minimization**: Only necessary data is stored and processed  
- **Access Control Awareness**: User roles and permissions are respected  
- **Separation of Public and Internal Assets**: Sensitive artifacts are not exposed  
- **Transparency**: All intentional omissions are documented clearly  

---

## Sensitive Data Exclusion

The following types of data are intentionally NOT included in this repository:

### 1. SharePoint Environment

- No screenshots of SharePoint lists  
- No internal site URLs  
- No tenant-specific configuration  
- No production data  

Instead, only:
- column names  
- schema structure  
- logical design  

are documented to allow safe replication.

---

### 2. Organizational Information

- No internal office identifiers  
- No company-sensitive layouts  
- No employee data  

All examples and references are generalized.

---

### 3. Email Infrastructure

- No real mailbox details  
- No SMTP configurations  
- No internal email templates  

Email behavior is described conceptually without exposing operational details.

---

## Floor Plan Handling

Floor layouts are part of the system functionality and are therefore included within the Power Apps export files (`.msapp`).

However:

- Floor plans are **not exposed as standalone images** in this repository  
- No screenshots of actual office layouts are published  

This approach ensures:

- the application remains functional when imported  
- sensitive internal layouts are not easily accessible or publicly visible  

---

## Power Apps Security Considerations

### 1. Client-Side Logic

- Validation logic is implemented in Power Fx  
- Includes checks for:
  - reservation limits  
  - desk availability  
  - user permissions  

---

### 2. Geofencing Enforcement

- Attendance confirmation is restricted to users physically present in the office  
- Prevents:
  - remote check-ins  
  - misuse of QR codes  

---

### 3. User Identity

- User identity is derived from the Power Apps `User()` function  
- Used for:
  - ownership validation  
  - access control logic  

---

## SharePoint Data Security

### 1. Controlled Access

In a production environment, SharePoint lists should be configured with:

- restricted access permissions  
- role-based visibility  
- limited edit rights  

---

### 2. Data Integrity

The system ensures:

- only one active reservation per desk per day  
- status-driven lifecycle management  
- controlled updates to reservation records  

---

### 3. Data Separation

Sensitive operational data is separated into:

- Active_Reservations → real-time data  
- Archived_Reservations → historical data  

This reduces exposure and improves control.

---

## Automation Security

Power Automate flows are designed to:

- trigger only under specific conditions  
- avoid unintended actions  
- prevent duplicate operations  

Flows rely on:

- status-based conditions  
- controlled triggers  
- structured data inputs  

---

## Repository-Level Security

This repository intentionally excludes:

- credentials  
- API keys  
- tenant-specific configurations  
- environment variables  

All shared content is:

- sanitized  
- generic  
- safe for public viewing  

---

## What Is Included

To maintain usability while preserving confidentiality, the repository includes:

- Power Apps `.msapp` files  
- SharePoint schema definitions  
- Power Fx logic  
- system design documentation  

This allows others to:
- understand the system  
- replicate the architecture  
- learn from the design  

without exposing sensitive data.

---

## Limitations of Public Sharing

Due to confidentiality constraints:

- full production environments cannot be replicated exactly  
- certain UI elements are not shown visually  
- some configurations must be recreated manually  

These limitations are intentional and necessary.

---

## Best Practices for Deployment

When deploying this system in a real environment:

- configure proper SharePoint permissions  
- restrict access to sensitive lists  
- use secure mailboxes for notifications  
- validate user roles (especially SuperUsers)  
- ensure compliance with organizational policies  

---

## Summary

Security and confidentiality were key considerations in both the system design and the public release of this project.

By:

- excluding sensitive data  
- limiting exposure of internal assets  
- documenting intentional omissions  
- preserving functional components  

the repository achieves a balance between:

- transparency  
- usability  
- security  

This ensures the system can be understood and replicated without compromising organizational integrity.