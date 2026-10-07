# Windows Server Group Policy (GPO) Configuration & Troubleshooting Lab

## Project Overview

This project demonstrates the configuration and management of **Group Policy Objects (GPOs)** using Windows Server 2022 and Windows 10 Enterprise virtual machines hosted in Microsoft Azure.

The objective was to centrally manage user settings, enforce security policies, verify policy application, and troubleshoot Group Policy issues in an Active Directory environment.

## Technologies Used

- Microsoft Azure
- Windows Server 2022 Datacenter: Azure Edition
- Windows 10 Enterprise
- Active Directory Domain Services (AD DS)
- Group Policy Management Console (GPMC)
- Command Prompt

## Lab Environment

```text
Microsoft Azure
│
├── Windows Server 2022 (SERVER01)
│   ├── Active Directory
│   ├── DNS Server
│   └── Group Policy Management
│
└── Windows 10 Enterprise (CLIENT01)
    └── Joined to davidlab.local
```

## Step 1: Verify Active Directory

I verified that my existing Active Directory domain, `davidlab.local`, was operational and contained the Organizational Units and user accounts created in my previous lab.

**Screenshot:**

<!-- Insert Active Directory screenshot here -->

## Step 2: Create a Control Panel Restriction GPO

Using Group Policy Management, I created a GPO named `IT - Restrict Control Panel` and linked it to the IT Organizational Unit.

I enabled the following setting:

```text
User Configuration
→ Policies
→ Administrative Templates
→ Control Panel
→ Prohibit access to Control Panel and PC settings
```

I tested the restriction using my Windows 10 domain user account.

**Screenshot:**

<!-- Insert Control Panel restriction screenshot here -->

## Step 3: Configure an Automatic Screen Lock Policy

I created another GPO named `IT - Screen Lock Policy` to enforce screen saver security settings.

Configured settings:

- Enable screen saver
- Password protect the screen saver
- Screen saver timeout: 300 seconds
- Force specific screen saver: `scrnsave.scr`

These settings require users to authenticate when returning from the screen saver.

**Screenshot:**

<!-- Insert screen saver GPO screenshot here -->

## Step 4: Configure Domain Password Policy

Using the Default Domain Policy, I configured password security requirements.

| Policy | Configuration |
|---|---|
| Minimum password length | 12 characters |
| Password complexity | Enabled |
| Password history | 5 passwords |

**Screenshot:**

<!-- Insert password policy screenshot here -->

## Step 5: Verify Group Policy Application

On my Windows 10 Enterprise VM, I refreshed Group Policy using:

```cmd
gpupdate /force
```

I verified the applied policies using:

```cmd
gpresult /r
```

I also generated an HTML report:

```cmd
gpresult /h "%USERPROFILE%\Desktop\GPO-Report.html" /f
```

This allowed me to confirm that the configured policies were being applied to the appropriate domain user.

**Screenshot:**

<!-- Insert gpresult screenshot here -->

## Step 6: Group Policy Troubleshooting

To simulate a real-world troubleshooting scenario, I temporarily disabled the link for the Control Panel restriction GPO.

I then refreshed Group Policy and checked the applied policies using:

```cmd
gpupdate /force
gpresult /r
```

After identifying the disabled GPO link, I re-enabled it and verified that the Control Panel restriction was restored.

**Screenshot:**

<!-- Insert troubleshooting screenshot here -->

## Skills Demonstrated

- Windows Server Administration
- Group Policy Object Configuration
- Active Directory Administration
- Organizational Unit Management
- Security Policy Enforcement
- Domain Password Policies
- Windows Client Administration
- Group Policy Troubleshooting
- `gpupdate` and `gpresult`
- Microsoft Azure

## What I Learned

This lab helped me understand how organizations use Group Policy to centrally manage Windows computers and user settings.

I gained practical experience creating and linking GPOs, enforcing security restrictions, verifying policy application, and troubleshooting Group Policy issues.

## Author

**David Saint Louis**  
Information Technology / Cybersecurity

[LinkedIn](https://www.linkedin.com/in/david-saint-louis-)
