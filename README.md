# User_Account_Password
Procedure on how to setup password attempt threshold, reset password, and unlock account when threshold is met in Active Directory on Azure.


<h2>Environments and Technologies Used</h2>

**Technologies and Servies**
- Microsoft Azure
- Active Directory Domain Services
- Group Policy

**Environment/Operating System**
- Windows Server 2022
- Windows 10

<h2>High-Level Deployment and Configuration Steps</h2>

**Step 1: Setup Group Policy**
- Login to DC-1 as an Admin (jane.doe)
- Open "Server Manager" > "Tools" on top left > "Group Policy Management".
- Go to "Forest:domanin name (mydomain.net)" > "Domains" > "Domain name (mydomain.net)" > right click "Default Domain Policy" > "Edit...".
- Go to "Computer Configuration" > "Policies" > Windows Settings" > "Security Settings" > "Account Policies" > "Account Lockout Policy".
- Select "Account Lockout Threshold", set for 5 attempts, and click "Apply".

![Account Lockout Threshold](https://github.com/user-attachments/assets/8e9e0df1-5f3f-441c-8b83-8b9a8bbb0021)

**Step 2: Update Group Policy**
- Login to Client-1 as Admin user(jane.doe).
- Open Commmand Prompt.
- Run gpupdate /force
  - This will update the group policy on Client-1 without waiting.

![Group Policy Update](https://github.com/user-attachments/assets/62ee4103-5499-4d46-a069-30b8a3a0daf3)

 
**Step 3: Attempt Login**
- Select a domain user and mistype the password 5 times.
- On the sixth try you will get a prompt of account is lock after multiple attempts.

![Account Lockout message](https://github.com/user-attachments/assets/cc62c2d6-c589-4b52-b7a2-91a5374d2868)

**Step 4: Unlock Account**
- Go back to DC-1
- Open "Server Manger" > "Tools" on top left > "Active Directory Users and Computers".
- Right-click your domain name (mydomain.net) and select "Find"
- Type the user's name you are looking for.
- Right-click the user's name and select "Reset Password..."
- Type new password (Password2), check "Unlock the user's account" box and click "OK".

![Reset Password](https://github.com/user-attachments/assets/f27b8b7b-5ab5-421f-8b89-e7bbb843baf3)

- Login to Client-1 with new password.
