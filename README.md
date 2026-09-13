# File Shares, Permissions, and Security Groups

This project demonstrates the configuration of **Windows network file shares**, permissions, and Active Directory security groups in a Microsoft Azure domain environment.

The lab covers shared folder permissions, access testing from a domain client, and group-based access control using Active Directory.

## Environments and Technologies Used

- Microsoft Azure
- Windows Server 2022
- Windows Client
- Active Directory Domain Services (AD DS)
- Windows File Sharing (SMB)
- NTFS / Share Permissions
- Active Directory Security Groups
- Remote Desktop (RDP)

## Prerequisites

- `DC-1` configured as a Domain Controller
- `Client-1` joined to `mydomain.com`
- Domain Administrator account
- Normal Domain User account

# Configuration Steps

## 1. Create Shared Folders

On `DC-1`, create the following folders on the `C:\` drive:

- `read-access`
- `write-access`
- `no-access`
- `accounting`

<p>
<img width="1280" height="682" alt="image" src="https://github.com/user-attachments/assets/5f6af081-2303-44de-b98c-22621b050b2e" />
</p>

## 2. Configure Share Permissions

Configure the following permissions:

### read-access

- Group: `Domain Users`
- Permission: `Read`

### write-access

- Group: `Domain Users`
- Permission: `Read / Write`

### no-access

- Group: `Domain Admins`
- Permission: `Read / Write`

The `accounting` folder will be configured later.

<p>
<img width="1290" height="792" alt="image" src="https://github.com/user-attachments/assets/a1e1601c-b96f-45da-bd6e-4402ad6e0ea7" />
</p>

## 3. Access the Shares from Client-1

Login to `Client-1` using a normal domain user.

Open:

`Win + R`

Enter:

`\\DC-1`

The shared folders hosted on DC-1 should appear.

<p>
<img width="1272" height="667" alt="image" src="https://github.com/user-attachments/assets/bc832873-bd8e-4d7d-8757-6110471f7bdb" />
</p>

## 4. Test User Permissions

Test access to each folder using the normal domain user.

Expected results:

- `read-access` → User can open and read files
- `write-access` → User can open, create, and modify files
- `no-access` → Access should be denied

<p>
<img width="1271" height="677" alt="image" src="https://github.com/user-attachments/assets/1feb67bf-e430-494e-a87b-f47c0b09d725" />
</p>

# Security Group Configuration

## 5. Create the ACCOUNTANTS Security Group

On `DC-1`, open:

`Active Directory Users and Computers`

Create a new Security Group named:

`ACCOUNTANTS`

<p>
<img width="862" height="607" alt="image" src="https://github.com/user-attachments/assets/e53539b8-79fe-4fe4-a8cc-ce9d8c770b96" />
</p>

## 6. Configure the Accounting Share

Configure the `accounting` folder with:

- Group: `ACCOUNTANTS`
- Permission: `Read / Write`

<p>
<img width="437" height="495" alt="image" src="https://github.com/user-attachments/assets/5f85f87f-2318-494a-9eb9-14d4a8e00437" />
</p>

## 7. Test Access Before Group Membership

From `Client-1`, attempt to access:

`\\DC-1\accounting`

using the normal domain user.

Access should be denied because the user is not yet a member of the `ACCOUNTANTS` security group.

<p>
<img width="1267" height="671" alt="image" src="https://github.com/user-attachments/assets/2c788986-9156-40df-9874-73868128b4e1" />
</p>

## 8. Add the User to ACCOUNTANTS

On `DC-1`, open Active Directory Users and Computers.

Add the normal domain user to:

`ACCOUNTANTS`

Log out of Client-1 and sign back in so the user's new group membership is applied.

<p>
<img width="1282" height="682" alt="image" src="https://github.com/user-attachments/assets/e2b037ea-89e8-4fa9-89c7-44d29485f989" />
</p>

## 9. Verify Access

From Client-1, access:

`\\DC-1\accounting`

The user should now be able to access the folder and create or modify files.

<p>
<img width="1282" height="682" alt="image" src="https://github.com/user-attachments/assets/7f580174-3222-4a10-8e73-02d5320212d9" />
</p>

## Skills Demonstrated

- Windows File Sharing (SMB)
- Active Directory administration
- User and group management
- Security Groups
- File and folder permissions
- Network share configuration
- Access control
- Permission troubleshooting
- Windows client/server administration

## Project Outcome

Successfully configured **Windows network file shares with different access levels** and implemented group-based access control using an Active Directory Security Group.

The lab demonstrates how administrators can control access to shared company resources based on user roles and group membership.
