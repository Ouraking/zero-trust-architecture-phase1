<img src="./repo-banner.svg" alt="Zero Trust Architecture: centralized IAM for 40,000 student identities" width="100%"/>

# Zero Trust Architecture - Phase 1

## Designing and Validating a Centralized Identity and Access Management Solution for 40,000 Student Identities

### Overview

This project addresses critical cybersecurity vulnerabilities at a large academic institution (40,000+ students) by designing, configuring, and testing a centralized Identity and Access Management (IAM) solution using **Microsoft Entra ID**.

### The Problem

The institution lacks basic cybersecurity controls:
- No centralized directory service
- Sequential student IDs used as both usernames and passwords
- No Multi-Factor Authentication (MFA)
- No institutional email infrastructure

### Solution

A proof-of-concept IAM deployment featuring:
- **25 simulated student identities** in Microsoft Entra ID
- **4 Conditional Access policies** enforcing MFA
- **IAM governance framework** aligned with NIST CSF 2.0 and ISO/IEC 27001:2022
- **PowerShell bulk provisioning** template for scaling to 40,000 users

### Architecture

```mermaid
%%{init: {'theme':'base','themeVariables':{'primaryColor':'#101A33','primaryTextColor':'#F2F6FF','primaryBorderColor':'#2DD4BF','lineColor':'#8B97B8','secondaryColor':'#0D1428','tertiaryColor':'#0A0F1E','clusterBkg':'#0A0F1E','clusterBorder':'#24335C','edgeLabelBackground':'#0D1428','fontSize':'14px'}}}%%
flowchart TB
    S["Student sign-in attempt"] --> ENT["Microsoft Entra ID<br/>central directory"]
    T1["PowerShell bulk provisioning"] --> T2["25 identities<br/>proof of concept"]
    T2 --> T3["40,000 identities<br/>staged rollout"]
    T3 -.->|"populates"| ENT

    ENT --> CA{"Conditional Access<br/>policy evaluation"}

    subgraph POL["4 Conditional Access policies, 100% enforcement in testing"]
        direction LR
        P1["Require MFA<br/>for all users"]
        P2["Block legacy<br/>authentication"]
        P3["Require compliant<br/>device"]
        P4["Session controls<br/>for risky sign-in"]
    end

    CA --> POL
    POL --> D{"All conditions<br/>satisfied?"}
    D -->|Yes| OK["Access granted to<br/>institutional resources"]
    D -->|No| BLOCK["Access blocked<br/>and logged"]

    classDef ok fill:#0D1428,stroke:#2DD4BF,stroke-width:2px,color:#AEE8DE
    classDef blocked fill:#0D1428,stroke:#F5B942,stroke-width:2px,color:#F5B942
    classDef core fill:#101A33,stroke:#2DD4BF,stroke-width:2px,color:#F2F6FF
    class OK ok
    class BLOCK blocked
    class ENT,CA core
```

### Frameworks & Standards

- NIST SP 800-207 (Zero Trust Architecture)
- NIST SP 800-30 Rev. 1 (Risk Assessment)
- NIST Cybersecurity Framework 2.0
- ISO/IEC 27001:2022
- Forrester Zero Trust Model

### Methodology

Design Science Research (DSR) methodology conducted within a controlled Microsoft Azure environment.

### Results

- 100% policy enforcement across all four Conditional Access scenarios
- Zero failures during testing
- Staged rollout strategy validated for scaling from 25 to 40,000 identities

### Phase 1 Scope

This Phase 1 implementation establishes the foundation for a broader Zero Trust transformation, including future:
- Network segmentation
- Endpoint management
- Advanced threat protection

### Documentation

- [Zero_Trust_IAM_Phase1_Proposal.docx](Zero_Trust_IAM_Phase1_Proposal.docx) - Full project documentation

### Tech Stack

- Microsoft Entra ID (Azure AD)
- Microsoft Azure
- PowerShell
- Conditional Access Policies
- Multi-Factor Authentication (MFA)
