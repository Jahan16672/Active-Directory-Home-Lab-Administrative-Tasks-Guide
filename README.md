# Active Directory Home Lab - Administrative Tasks Guide

## Overview

This documentation covers essential Active Directory administrative tasks in a home lab environment. The lab assumes you have already installed Windows Server with Active Directory Domain Services and have Windows client VMs joined to the domain.

## Prerequisites

- Windows Server with Active Directory Domain Services installed and configured
- Domain Controller properly set up
- Windows client VMs joined to the domain
- Administrative access to the domain

## Table of Contents

1. [Finding Objects in Active Directory](#1-finding-objects-in-active-directory)
2. [Password Reset Operations](#2-password-reset-operations)
3. [Managing User Profiles and Group Memberships](#3-managing-user-profiles-and-group-memberships)
4. [Moving Objects Between Organizational Units](#4-moving-objects-between-organizational-units)
5. [Advanced Features and Attribute Editing](#5-advanced-features-and-attribute-editing)
6. [Service Account Management](#6-service-account-management)
7. [User Onboarding and Offboarding](#7-user-onboarding-and-offboarding)

---

## 1. Finding Objects in Active Directory

Active Directory Users and Computers (ADUC) allows you to locate and manage various directory objects.

### Step-by-Step Process:

1. **Open Active Directory Users and Computers**
   - Start → Administrative Tools → Active Directory Users and Computers
   - Or run `dsa.msc` from Run dialog

2. **Navigate the Directory Structure**
   - Expand your domain in the left pane
   - Browse through Organizational Units (OUs)

3. **Locate Different Object Types:**
   - **Users**: Found in Users container or custom OUs
   - **Computers**: Located in Computers container or domain OUs
   - **Printers**: Typically in custom OUs or the domain root

4. **Use Search Functionality**
   - Right-click on domain → Find
   - Select object type (Users, Computers, Printers)
   - Enter search criteria
     
![image](https://github.com/user-attachments/assets/1a7c4175-9c49-4547-ba94-05c7fb2f59f5)

***Ref-1 Finding Objects in Active Directory***

---

## 2. Password Reset Operations

Password resets are common administrative tasks that require proper security considerations.

### Step-by-Step Process:

1. **Locate the User Account**
   - Navigate to the appropriate OU containing the user
   - Find the target user account

2. **Initiate Password Reset**
   - Right-click on the user account
   - Select "Reset Password" from context menu

![image](https://github.com/user-attachments/assets/be26e204-f739-4936-a9d3-7634fa1f91b1)

***Ref-2 Initiate Password Reset***

3. **Set New Password**
   - Enter the new password
   - Confirm the password
   - **Important**: Check "User must change password at next logon"

4. **Unlock Account (If Necessary)**
   - ✅ **Always verify**: Check "Unlock the user's account" if the account is locked
   - This step is crucial for locked accounts

5. **Apply Changes**
   - Click OK to confirm the password reset
   - Notify the user of the temporary password

![image](https://github.com/user-attachments/assets/1a3c25e1-6285-4db8-9a1d-67cb9b723428)

***Ref-3 Password Reset Interface***

### Security Best Practices:
- Always require password change on next logon
- Use complex temporary passwords
- Verify user identity before resetting passwords
- Document password reset activities

---

## 3. Managing User Profiles and Group Memberships

User profile management and group memberships are essential for access control and resource management.

### Adding Users to Groups:

1. **Access User Properties**
   - Right-click on user account → Properties
   - Navigate to "Member Of" tab

2. **Add Group Memberships**
   - Click "Add" button
   - Type group names or click "Advanced" to search
   - Select appropriate groups
   - Click OK to apply changes

![image](https://github.com/user-attachments/assets/bdf13806-eed3-46d0-9525-a8fe8bf87e89)

***Ref-4 Add group memberships***


3. **Verify Memberships**
   - Review the group list in "Member Of" tab
   - Ensure user has appropriate access levels

### Profile Management:
- Configure profile paths if using roaming profiles
- Set home directory locations
- Manage logon scripts through Group Policy

---

## 4. Moving Objects Between Organizational Units

Moving objects between OUs is common when users change departments or roles.

### Example Scenario: Moving Terry Smith from HR to IT Department

1. **Locate the User**
   - Navigate to HR OU
   - Find Terry Smith's user account

2. **Initiate Move Operation**
   - Right-click on Terry Smith
   - Select "Move..." from context menu

3. **Select Destination OU**
   - Browse to IT department OU
   - Select the target container
   - Click OK to confirm move

![image](https://github.com/user-attachments/assets/f512467f-5496-4be3-9cc3-0f6a3ece7cb2)

***Ref-5 Select Destination OU***

4. **Verify Move**
   - Navigate to IT OU
   - Confirm Terry Smith appears in new location
   - Check that group memberships are still appropriate

### Important Considerations:
- Group Policy settings may change based on new OU
- Update group memberships if department-specific groups exist
- Notify user of any access changes

---

## 5. Advanced Features and Attribute Editing

Advanced features provide granular control over Active Directory objects.

### Enabling Advanced Features:

1. **Access Advanced View**
   - In ADUC, go to View menu
   - Select "Advanced Features"
   - This reveals additional containers and properties

![image](https://github.com/user-attachments/assets/24c67e91-010b-45f0-8f96-f27e11453a35)

***Ref-6 Advanced View***

2. **Using Attribute Editor**
   - Right-click on any object → Properties
   - Navigate to "Attribute Editor" tab
   - View and modify advanced object attributes

### Attribute Editor Functions:
- **Filter**: Show only set attributes or all attributes
- **Edit**: Modify attribute values directly
- **Syntax**: View attribute data types and constraints

![image](https://github.com/user-attachments/assets/b408b9c0-f2c4-4a84-bf6a-a9cf642a8beb)

***Ref-7 Attribute editor***

### Computer Properties Management:
- Access computer objects with enhanced properties
- Manage computer-specific attributes
- Configure delegation settings

### Use Cases:
- Troubleshooting replication issues
- Setting custom attributes for applications
- Advanced security configurations

---

## 6. Service Account Management

Service accounts are specialized accounts used by applications and services.

### Service Account vs User Account:

| Feature | User Account | Service Account |
|---------|-------------|-----------------|
| Purpose | Human users | Applications/Services |
| Interactive Logon | Yes | Usually No |
| Password Policy | Standard | Often complex/long |
| Management | Regular maintenance | Set and forget |

### Creating Service Accounts:

1. **Create New User**
   - Right-click in appropriate OU → New → User
   - Use naming convention (e.g., svc_application_name)

2. **Configure Service Account Properties**
   - Set strong, complex password
   - Configure "Password never expires" if required
   - Set "User cannot change password"
   - Disable "User must change password at next logon"

![image](https://github.com/user-attachments/assets/083e44a1-1c98-44c4-9425-811a97e5ff1b)

***Ref-8 Creating Service account***

3. **Security Considerations**
   - Use Managed Service Accounts (MSA) when possible
   - Implement least privilege principles
   - Regular password rotation for traditional service accounts

---

## 7. User Onboarding and Offboarding

Efficient user lifecycle management ensures security and productivity.

### Onboarding New Users:

#### Method 1: Copy Existing User Template

1. **Select Template User**
   - Find existing user with similar role (e.g., Terry with multiple group memberships)
   - Right-click → Copy

2. **Create New User**
   - Enter new user details
   - Password settings
   - Account options

3. **Verify Group Memberships**
   - Check copied group memberships
   - Adjust as necessary for new user's role

![image](https://github.com/user-attachments/assets/8e63feb0-53df-425b-9f0a-2866ac4af799)

***Ref-9 Moving Group Memberships***

#### Method 2: Manual Creation

1. **Create User Account**
   - Right-click OU → New → User
   - Complete user information

2. **Configure Properties**
   - Set appropriate group memberships
   - Configure profile settings
   - Set organizational information

### Offboarding Users:

1. **Disable Account**
   - Right-click user → Disable Account
   - Prevents immediate access

2. **Remove Group Memberships**
   - Keep only basic domain user groups
   - Document removed memberships

3. **Move to Disabled OU**
   - Create separate OU for disabled accounts
   - Move account for organization

4. **Data Backup**
   - Backup user profile and home directory
   - Transfer ownership of files if needed

---

## Best Practices and Security Considerations

### General Best Practices:
- Use descriptive names for OUs and groups
- Implement consistent naming conventions
- Regular auditing of group memberships
- Document all administrative changes
- Use Group Policy for standardized configurations

### Security Considerations:
- Principle of least privilege
- Regular password policy enforcement
- Monitor administrative actions
- Implement proper delegation of permissions
- Regular security audits and reviews

### Troubleshooting Tips:
- Check Event Viewer for authentication issues
- Verify DNS resolution for domain operations
- Use `gpupdate /force` after policy changes
- Monitor replication health between domain controllers

---

## Conclusion

This guide covers fundamental Active Directory administrative tasks essential for managing a domain environment. Regular practice of these procedures ensures efficient user and resource management while maintaining security best practices.

For advanced scenarios, consider implementing:
- Group Policy management
- Advanced security features
- Automated user provisioning
- Integration with cloud services

---

## Additional Resources

- Microsoft Active Directory Documentation
- PowerShell Active Directory Module
- Group Policy Management Console
- Active Directory Administrative Center

> **Note**: This documentation is based on a home lab environment. Production environments may require additional security considerations and change management procedures.
