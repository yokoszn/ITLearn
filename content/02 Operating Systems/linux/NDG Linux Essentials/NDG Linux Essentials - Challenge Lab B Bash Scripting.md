[[Personal Learning]][[Linux]] [[scripts]]
## Instructions

### Case Scenario

In the User Management challenge lab, you were tasked with creating users and groups. Using the commands one at a time from the command line can be a tedious process and could lead to potential errors in syntax. It is your duty, as an administrator, to make the process as seamless and efficient as possible.

### Objectives

Create a bash script to perform user management tasks as outlined below:

- Create a new group. Each group must have a unique name. The script must check to ensure that no duplicate group names exist on the system. If a duplicate is found, an error needs to be reported, and the administrator must try another group name.
- Create a new user. Each user must have a unique name. The script must check to ensure that no duplicate usernames exist on the system. If a duplicate is found, an error needs to be reported and the administrator must try another username. The user will have a Bash login shell and belong to the group that was created in the previous step.
- Create a password for each user that is created.
- Ensure that the new user created is a member of the new group created.
- Create a directory at the root `/` of the file system with same name as the user created.
- Set the ownership of the directory to the user and group created.
- Set the permissions of the directory to full control for the owner and full control for the group created.
- Set the permissions to ensure that only the owner of a file can delete it from the directory.
- Ensure that the script is executable.

This script should be designed to accept any username and any group name. **DO NOT hardcode commands to create specific usernames and group names.**

### Hints

- Logical order is important.
- There is a special wildcard that can be used to determine if the previous command is successful or not. This will be useful for this script.

### Curriculum Resources

- Module 11 – Basic Scripting
- Module 16 – Creating Users and Groups
- Module 17 – Ownership and Permissions

### Deliverables

- Execute the script for the instructor. Create a new unique user and new unique group.
- Execute the script for the instructor. Show the error when a duplicate user or duplicate group are created.

----


## Answer Key

Below is a sample of the bash script.

Keep in mind that this script is just an example; it may be done many different ways. Scripts developed by students to meet the objectives and deliverables of this lab will vary.

echo -n "Enter the username for the new user:"                                  
read username                                                                   
                                                                                
getent passwd $username >> /dev/null                                            
                                                                                
while [ $? -eq 0 ]                                                              
  do                                                                            
    echo -n "User already created\n"                                            
    echo -n "Please enter another username: "                                   
    read username                                                               
    getent passwd $username >> /dev/null                                        
  done                                                                          
                                                                                
echo -n "Enter a group name: \n"                                                
read groupname                                                                  
                                                                                
getent group $groupname >> /dev/null                                            
                                                                                
while [ $? -eq 0 ]                                                              
  do                                                                            
   echo -e "Group already exists\n"                                             
   echo -e "Please enter another group name: \n"                                
   read groupname                                 
   getent group $groupname >> /dev/null                                         
  done                                                                 
                                                                                
groupadd $groupname                                                             
useradd -m -s /bin/bash -g $groupname $username 
passwd $username                              
                                                                                
echo -n "User created\n"                                                       
                                                                                
mkdir /$username                                                                
chown $username.$groupname /$username                                           
chmod 1770 /$username

---




---


To confirm if the script worked correctly, you can perform several checks on the system to ensure that each step completed as expected. Here are the steps you can take to verify each aspect of the script:

### 1. **Check if the Group was Created**

- Use the `getent group` command to verify that the group was created successfully.

bash

Copy code

`getent group groupname`

- Replace `groupname` with the name of the group you created. If the group exists, this command will return the group entry. If it doesn't exist, there will be no output.

### 2. **Check if the User was Created**

- Use the `id` command to verify that the user was created and added to the correct group.

bash

Copy code

`id username`

- Replace `username` with the name of the user you created. The output should show the user ID (`uid`), group ID (`gid`), and the groups the user belongs to, including the group created in the previous step.

### 3. **Check User's Shell and Home Directory**

- Verify that the user has the correct shell and home directory.

bash

Copy code

`getent passwd username`

- This command will display the user's information, including the home directory and shell. You should see `/bin/bash` as the shell and the correct home directory.

### 4. **Verify the User's Password**

- Ensure the user's password was set by attempting to switch to the new user.

bash

Copy code

`su - username`

- Enter the password you set for this user. If the password is correct, this command should log you in as the new user. If it fails, there may have been an issue with setting the password.

### 5. **Check the Directory Creation and Permissions**

- Verify the existence of the directory created for the user in the root directory.

bash

Copy code

`ls -ld /username`

- Replace `username` with the user's name. This command will display the directory's details, including permissions and ownership. The expected output should show the following:
    - Directory exists at the root (`/`).
    - Permissions should be `drwxrwx--T`, indicating the sticky bit is set (restricts file deletion to the owner).
    - Ownership should be the newly created user and group.

### 6. **Check File Deletion Restrictions (Sticky Bit)**

- As another user, try creating and deleting files in the directory to confirm the sticky bit.

bash

Copy code

`touch /username/testfile rm /username/testfile`

- If the sticky bit is correctly set, only the owner (or root) can delete the file. Non-owner users should get a "Permission denied" error when attempting to delete the file.

### 7. **Review the System Logs (Optional)**

- You can check the system logs to see if there are any errors or messages related to user and group creation.

bash

Copy code

`tail /var/log/auth.log`

- On some systems, the log file might be different (e.g., `/var/log/secure` for RHEL-based systems). Look for entries related to the commands used in the script.

### Summary of Confirmation Steps

1. **Group Creation**: Use `getent group groupname`.
2. **User Creation**: Use `id username` and `getent passwd username`.
3. **Password**: Try switching to the user with `su - username`.
4. **Directory and Permissions**: Use `ls -ld /username`.
5. **Sticky Bit**: Test file deletion by non-owners.

By performing these checks, you can confirm that each part of the script worked correctly and that the user, group, directory, and permissions were set up as expected.

---

[[Bash Script - user_management.sh]]