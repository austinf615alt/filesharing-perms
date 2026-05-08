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
- File Explorer

<h2>Operating Systems Used </h2>

- Windows Server 2025 Datacenter X64 Gen2

<h2>High-Level Configuration Steps</h2>

- Step 1: Configured File Share Permissions
- Step 2: Tested Access from Client Machine
- Step 3: Created and Configured Security Group in Active Directory
- Step 4: Assigned Group Membership and Verified Access Control

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="2287" height="1223" alt="LAB7-CONFIGURINGFILESHAREPERMS" src="https://github.com/user-attachments/assets/bf3405f2-a7b4-4e2c-a2aa-5ca3743758d5" />
</p>
<p>

- Remoted into both the Client-1 Virtual Machine and the Domain-Controller Virtual Machine using Remote Desktop Connection. Used the public IP address given to each respective Virtual Machine to sign in, signing into Domain-Controller with a domain administrator account and Client-1 with a non-administrator domain account.
  
- Created multiple shared folders on the C:\ drive of Domain-Controller to simulate different access levels. Configured folder sharing and NTFS permissions to control access for different security groups such as "Domain Users" and "Domain Admins", assigning different levels of access to each such as "read-only" and "read/write" to demonstrate role-based file share permissions in a domain environment.

</p>
<br />

<p>
<img width="1729" height="1002" alt="LAB7-PERMTESTCLIENT" src="https://github.com/user-attachments/assets/95cc62fd-9363-438c-9866-e2d404f4e756" />
</p>
<p>

- On Client-1 Virtual Machine, as a non-administrator domain account accessed the shared folders on Domain-Controller using the network path (\\Domain-Controll). Tested access to each shared folder to validate the configured permissions. Confirmed that the access levels behaved as configured for each folder, demonstrating the proper enforcement of access controls in the domain.

</p>
<br />

<p>
<img width="2287" height="1223" alt="LAB7-ACCOUNTANTSETUP" src="https://github.com/user-attachments/assets/1aa4d42b-583b-4802-b5d4-97b025a4fd67" />
</p>
<p>

- On Domain-Controller Virtual Machine, as a domain administrator added and configured a security group called "ACCOUNTANTS" inside of Active Directory Users and Groups. On the accounting folder within the C:\ drive, configured sharing properties and added the group "ACCOUNTANTS" and gave Read/Write permissions.

</p>
<br />

<p>
<img width="2287" height="1223" alt="LAB7-ACCOUNTINGCLIENT" src="https://github.com/user-attachments/assets/6b6ec63d-df35-4ea7-89af-17971e6f4aa9" />
</p>
<p>

- On Client-1 Virtual Machine, as the non-administrator domain user, attempted to access the accounting folder. Note it fails, as this user has not been added to the "ACCOUNTANTS" group within the domain, therefore has no access to the accounting folder.

</p>
<br />

<p>
<img width="2287" height="1223" alt="LAB7-ACCOUNTINGCLIENTFIX" src="https://github.com/user-attachments/assets/e5e86bf1-7531-4a1e-a256-014bb9b12d71" />
</p>
<p>

- On Domain-Controller Virtual Machine, add the non-administrator domain user (baboro.Jim in this case) within the "ACCOUNTANTS" security group within Active Directory Users and Groups. 
  
</p>
<br />

<p>
<img width="2287" height="1223" alt="LAB7-ACCOUNTINGCLIENTFINAL" src="https://github.com/user-attachments/assets/e3f74800-f7f6-4992-9918-66cc85a2bd9b" />
</p>
<p>

- On Client-1 Virtual Machine, as the non-administrator, attempted to access the accounting folder again within (\\Domain-Controll). Observe that the user now has access to the folder since they are in the "ACCOUNTANTS" security group which has both read/write permissions.

</p>
<br />
