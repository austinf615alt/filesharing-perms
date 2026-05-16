<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Windows File Sharing and Permissions</h1>
This project outlines the implementation of File Sharing and Permissions within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Active Directory Users and Computers

<h2>Operating Systems Used </h2>

- Windows 11 Pro version 25H2 (For Azure and Remote Desktop)
- Windows Server 2025 Datacenter X64 Gen2 (x2 for Client VM and Domain Controller VM)

<h2>High-Level Configuration Steps</h2>

- Step 1: Configured Network File Shares and Access Permissions
- Step 2: Test Shared Folder Access as a Standard Domain User
- Step 3: Create and Apply Role-Based Security Group Permissions
- Step 4: Verify Access Changes through Group Membership Assignment

<h2>Deployment and Configuration Steps</h2>

---

## Step 1: Configured Network File Shares and Access Permissions

---

<p>
<img width="1624" height="979" alt="AD-VM Login" src="https://github.com/user-attachments/assets/9f43c302-81a2-4b3a-8f26-787fb0d203e7" />
</p>
<p>

- Connected to the Domain-Controller virtual machine using domain administrative credentials (jane_admin) to configure shared folders and access permissions.

<br />

<p>
<img width="1624" height="974" alt="AD-VM Folder Add" src="https://github.com/user-attachments/assets/1731a60c-eef9-4b44-99ef-46f6bc18c798" />
</p>
<p>

- Opened File Explorer on the domain controller and created four shared folders: read-access, write-access, no-access, and accounting to simulate different access control scenarios.

</p>
<br />

<p>
<img width="1624" height="974" alt="AD-VM Folder Verify" src="https://github.com/user-attachments/assets/a59df72b-b16a-4663-b254-64b9e7fe6b78" />
</p>
<p>

- Verified successful creation of the shared folders prior to configuring access permissions. The accounting folder was intentionally left unconfigured initially for later access control testing.
  
</p>
<br />

<p>
<img width="1624" height="974" alt="AD-VM WA Perms" src="https://github.com/user-attachments/assets/861ea84e-84c5-46a7-915b-5bc315b4bb43" />
</p>
<p>

- Shared the write-access folder and assigned Domain Users read and write permissions, allowing standard users to both access the folder and create or modify files.

</p>
<br />

<p>
<img width="1624" height="974" alt="AD-VM RA Perms" src="https://github.com/user-attachments/assets/ca236735-4882-476f-bd2c-93289b34e10f" />
</p>
<p>

- Shared the read-access folder and assigned Domain Users read-only permissions, allowing users to access folder contents without the ability to create or modify files.

</p>
<br />

<p>
<img width="1624" height="974" alt="AD-VM NA Perms" src="https://github.com/user-attachments/assets/cdef5d9b-49f6-4ada-847f-ea5c0e5282b0" />
</p>
<p>

- Shared the no-access folder and restricted access to the Domain Admins security group, preventing standard domain users from accessing the folder while allowing administrative access.

</p>
<br />

---

## Step 2: Test Shared Folder Access as a Standard Domain User

---

<p>
<img width="1624" height="974" alt="Client-1 NA Attempt" src="https://github.com/user-attachments/assets/a594060d-a18f-47df-801c-13c85cf483e3" />
</p>
<p>

- Logged into the client system using a standard domain user account and attempted to access the no-access shared folder, confirming that access was correctly denied due to insufficient permissions. Only domain admins have permissions.

</p>
<br />

<p>
<img width="1624" height="974" alt="Client-1 RA Attempt" src="https://github.com/user-attachments/assets/82a6f120-bc74-42c4-a0e1-f9bfe6af2da7" />
</p>
<p>

- Tested access to the read-access folder as a standard domain user, confirming that the folder could be opened but files could not be created or modified due to read-only permissions.

</p>
<br />

<p>
<img width="1624" height="974" alt="Client-1 WA Attempt" src="https://github.com/user-attachments/assets/91e682f0-4f63-495c-8183-9cdf0fbaad39" />
</p>
<p>

- Tested access to the write-access folder as a standard domain user, confirming successful read and write access by creating a test file within the shared folder.

</p>
<br />

---

## Step 3: Create and Apply Role-Based Security Group Permissions

---

<p>
<img width="1624" height="974" alt="AD-VM ADUC" src="https://github.com/user-attachments/assets/bdc7d7c4-b671-4b41-8b04-060f605c1505" />
</p>
<p>

- Accessed Active Directory Users and Computers (ADUC) from the domain controller to create a new security group for role-based file access management.

</p>
<br />

<p>
<img width="1624" height="974" alt="AD-VM Add Group Nav" src="https://github.com/user-attachments/assets/d40184a8-2ce1-47c5-a19e-056e85580997" />
</p>
<p>

- Navigated within Active Directory to the domain structure to begin creating a new security group.

</p>
<br />

<p>
<img width="1624" height="974" alt="AD-VM ACT Create" src="https://github.com/user-attachments/assets/ed4e6fa1-feb9-4737-a556-f9ec7aa51e43" />
</p>
<p>

- Created a new security group named ACCOUNTANTS to simulate department-based access control for shared file resources.

</p>
<br />

<p>
<img width="1624" height="974" alt="AD-VM ACT Only Perms" src="https://github.com/user-attachments/assets/9466d8a0-c180-4b6f-9f61-89539163aa7c" />
</p>
<p>

- Shared the accounting folder and assigned the ACCOUNTANTS security group read and write permissions, restricting access to authorized group members only.

</p>
<br />

---

## Step 4: Verify Access Changes through Group Membership Assignment

---

<p>
<img width="1624" height="974" alt="Client-1 ACT Attempt" src="https://github.com/user-attachments/assets/a5233d5e-d7e1-4655-97e7-40511212d7c6" />
</p>
<p>

- Attempted to access the accounting shared folder using a standard domain user account that was not a member of the ACCOUNTANTS group, confirming that access was correctly denied.

</p>
<br />

<p>
<img width="1624" height="974" alt="AD-VM ACT User Add" src="https://github.com/user-attachments/assets/8f0862db-95fc-428c-9da4-5ce3afb26a6a" />
</p>
<p>

- Added the standard domain user account to the ACCOUNTANTS security group in Active Directory to grant access to the accounting file share.

</p>
<br />

<p>
<img width="1624" height="981" alt="Client-1 ACT Success" src="https://github.com/user-attachments/assets/ccdb27bf-91c1-4d8a-9f80-f712d2119856" />
</p>
<p>

- Logged back into the client system using the updated domain user account and verified successful access to the accounting shared folder, confirming that security group membership changes were applied correctly.

</p>
<br />

---

## Skills Developed

### Windows File Sharing Administration

Gained hands-on experience creating and configuring shared folders within a Windows Server environment to support controlled network file access.

### File and Share Permission Management

Configured shared folder permissions with varying access levels, including read-only, read/write, and restricted administrative access, to simulate real-world access control scenarios.

### Active Directory Security Group Management

Created and managed Active Directory security groups to control access to shared resources based on user role and group membership.

### Role-Based Access Control (RBAC) Fundamentals

Developed practical experience implementing role-based access controls by assigning permissions to security groups rather than individual users.

### User Access Troubleshooting

Tested shared folder access from a standard domain user account to validate permissions, identify access restrictions, and confirm expected behavior.

### Identity and Access Management (IAM) Concepts

Applied core IAM concepts including permission assignment, group membership access control, authentication validation, and access provisioning.

### Remote Desktop Administration

Used Remote Desktop Protocol (RDP) to remotely access and manage both server and client virtual machines within the lab environment.

### Active Directory Administration

Used Active Directory Users and Computers (ADUC) to create security groups, manage user memberships, and apply access control changes.

### Access Validation and Permission Testing

Verified access changes by testing folder access before and after security group membership updates, confirming correct permission inheritance and access behavior.

### Windows Server Administration

Worked within a Windows Server environment to manage shared resources, user access, and network file services.

### Technical Documentation

Documented file sharing configuration, permission assignments, access testing, and security group workflows using structured technical documentation and screenshots.
