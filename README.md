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

I verified that my existing Active Directory domain, `mydomain.com`, was operational and contained the Organizational Units and user accounts created in my previous lab.


<img width="1470" height="956" alt="Screenshot 2026-10-07 at 6 19 52 PM" src="https://github.com/user-attachments/assets/bfa20460-d510-4ea3-9071-bb0a26bfccdd" />



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

<img width="1470" height="956" alt="Screenshot 2026-10-07 at 6 29 49 PM" src="https://github.com/user-attachments/assets/045a4910-c58e-4a2e-a7ed-29abf23ea3f7" />

## Step 3: Configure an Automatic Screen Lock Policy

I created another GPO named `IT - Screen Lock Policy` to enforce screen saver security settings.

Configured settings:

- Enable screen saver
- Password protect the screen saver
- Screen saver timeout: 300 seconds
- Force specific screen saver: `scrnsave.scr`

These settings require users to authenticate when returning from the screen saver.

<img width="1470" height="956" alt="Screenshot 2026-10-07 at 6 34 16 PM" src="https://github.com/user-attachments/assets/fcfc83f9-7d95-4095-96d5-06af70207b47" />
<img width="1470" height="956" alt="Screenshot 2026-10-07 at 6 56 03 PM" src="https://github.com/user-attachments/assets/822b0ba1-ca85-49a2-99d3-86e25572106a" />


## Step 4: Configure Domain Password Policy

Using the Default Domain Policy, I configured password security requirements.

| Policy | Configuration |
|---|---|
| Minimum password length | 12 characters |
| Password complexity | Enabled |
| Password history | 5 passwords |


<img width="1470" height="956" alt="Screenshot 2026-10-07 at 7 03 05 PM" src="https://github.com/user-attachments/assets/76aaea0f-a838-45d6-bf4f-a072115d1ff2" />


## Step 5: Verify Group Policy Application

On my Windows 10 Enterprise VM, I refreshed Group Policy using:

```cmd
gpupdate /force
```

I verified the applied policies using:

```cmd
gpresult /r
```

This allowed me to confirm that the configured policies were being applied to the appropriate domain user.

<img width="1470" height="956" alt="Screenshot 2026-10-07 at 7 05 43 PM" src="https://github.com/user-attachments/assets/eb2a67dc-9ca3-462b-a06a-ac76f0f8b07a" />


## Step 6: Group Policy Troubleshooting

To simulate a real-world troubleshooting scenario, I temporarily disabled the link for the Control Panel restriction GPO.

I then refreshed Group Policy and checked the applied policies using:

```cmd
gpupdate /force
gpresult /r
```

After identifying the disabled GPO link, I re-enabled it and verified that the Control Panel restriction was restored.


<img width="1470" height="956" alt="Screenshot 2026-10-07 at 7 12 18 PM" src="https://github.com/user-attachments/assets/08847e06-2297-4fb0-88a9-19fb0ae51432" />

<img width="1470" height="956" alt="Screenshot 2026-10-07 at 7 12 33 PM" src="https://github.com/user-attachments/assets/137d578f-3f92-4360-b07e-a89fa01b9d5e" />

<img width="1470" height="956" alt="Screenshot 2026-10-07 at 7 13 59 PM" src="https://github.com/user-attachments/assets/526eb6e8-aec5-44e9-a76c-15d89a9861b3" />


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


