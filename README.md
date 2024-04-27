# Use-Linux-commands-to-manage-file-permissions
Examine existing permissions on the file system, determine if the permissions match the authorization that should be given. If they do not match, modify the permissions to authorize the appropriate users and remove any unauthorized access.

## Table of contents

1. [Project description](#description)
2. [Check file and directory details](#details)
3. [Change file permissions](#permissions)
4. [Change file permissions on a hidden file](#permissions2)
5. [Change directory permissions](#permissions3)
6. [Summary](#permissions4)

## Project description <a name="description">
You are a security professional at a large organization. You mainly work with their research team. Part of your job is to ensure users on this team are authorized with the appropriate permissions. This helps keep the system secure. 

Your task is to examine existing permissions on the file system. You’ll need to determine if the permissions match the authorization that should be given. If they do not match, you’ll need to modify the permissions to authorize the appropriate users and remove any unauthorized access.

### Current file permissions
Below is the file structure of the `/home/researcher2/projects` directory
and the permissions of the files and subdirectory it contains.
In the `/home/researcher2/projects` directory, there are five files with the following
names and permissions:
* `project_k.txt`
  * User = read, write,
  * Group = read, write
  * Other = read, write
* `project_m.txt`
  * User = read, write
  * Group = read
  * Other = none
* `project_r.txt`
  * User= read, write
  * Group = read, write
  * Other = read
* `project_t.txt`
  * User = read, write
  * Group = read, write
  * Other = read
* `.project_x.txt`
  * User = read, write
  * Group = write
  * Other = none

There is also one subdirectory inside the `projects` directory named `drafts`. The
permissions on `drafts` are:
* User = read, write, execute
* Group = execute
* Other = none

## Check file and directory details <a name="details">
All commands used in this project will be Linus-based commands. Please research your OS's (Operating System) commands to get the same information.

From the CLI (Command Line Interface) type `ls` to see the list of contents of the current directory.

>researcher2@ee38eb1d384a:~$ `ls`
projects

Navigate to the `projects` directory. 
* `cd projects`
>researcher2@2dfe8e5aabad:~$ `cd projects`

List the contents and permissions of the `projects` directory.
* To list out the contents of the directory, use the same command as above but add a modifier to give the contents of the directories permissions
* `ls -l`
>researcher2@ee38eb1d384a:~$ `cd projects`  
researcher2@ee38eb1d384a:~/projects$ `ls -l`   
total 20  
drwx--x--- 2 researcher2 research_team 4096 Apr 27 18:30 drafts  
-rw-rw-rw- 1 researcher2 research_team   46 Apr 27 18:30 project_k.txt  
-rw-r----- 1 researcher2 research_team   46 Apr 27 18:30 project_m.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 18:30 project_r.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 18:30 project_t.txt  

If we use the `ls` without the `-l` modifier, we are presented with:
>researcher2@ee38eb1d384a:~/projects$ `ls`  
drafts  project_k.txt  project_m.txt  project_r.txt  project_t.txt  

As you can see above, it lists the same contents within the directory with less information. We must look at one of them to understand what the `-l` modifier provides.

`drwx--x---` 2 researcher2 research_team 4096 Apr 27 16:40 drafts

* The 1st character indicates the file type. The `d` indicates it’s a directory. When this character is a hyphen `-`, it's a regular file.
* The 2nd-4th characters indicate the read `r`, write `w`, and execute `x` permissions for the user. When one of these characters is a hyphen `-` instead, it indicates that this permission is not granted to the user.
* The 5th-7th characters indicate the read `r`, write `w`, and execute `x` permissions for the group. When one of these characters is a hyphen `-` instead, it indicates that this permission is not granted for the group.
* The 8th-10th characters indicate the read `r`, write `w`, and execute `x` permissions for the owner type of other. This owner type consists of all other users on the system apart from the user and the group. When one of these characters is a hyphen `-` instead, that indicates that this permission is not granted for other.

drwx--x--- `2 researcher2` `research_team` 4096 Apr 27 16:40 drafts

* The second block of text in the expanded directory listing is the user who owns the file.
* The third block of text is the group owner of the file.

If we would like to see if there are any hidden files, we can add the `-a` modifier 
* `ls -a`

>researcher2@ee38eb1d384a:~/projects$ `ls -a`   
.  ..  .project_x.txt  drafts  project_k.txt  project_m.txt  project_r.txt  project_t.txt  

We can also combine the `-l` modifier with `-a` to get the full list and permissions details  as well
* `ls -la`

>researcher2@2dfe8e5aabad:~/projects$ `ls -la`  
total 32  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 18:09 .  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 19:01 ..  
-rw--w---- 1 researcher2 research_team   46 Apr 27 18:09 .project_x.txt  
drwx--x--- 2 researcher2 research_team 4096 Apr 27 18:09 drafts   
-rw-rw-rw- 1 researcher2 research_team   46 Apr 27 18:09 project_k.txt  
-rw-r----- 1 researcher2 research_team   46 Apr 27 18:09 project_m.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 18:09 project_r.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 18:09 project_t.txt  

From the above screenshots, you will see that `.project_x.txt` is the hidden file in the directory.

>researcher2@e587efd88d96:~/projects$ `ls -l`  
total 20  
drwx--x--- 2 researcher2 research_team 4096 Apr 27 17:29 drafts  
-rw-rw-rw- 1 researcher2 research_team   46 Apr 27 17:29 project_k.txt  
-rw-r----- 1 researcher2 research_team   46 Apr 27 17:29 project_m.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_r.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_t.txt  

>researcher2@e587efd88d96:~/projects$ `ls -la`  
total 32  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 17:29 .  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 18:01 ..  
`-rw--w---- 1 researcher2 research_team   46 Apr 27 17:29 .project_x.txt`  
drwx--x--- 2 researcher2 research_team 4096 Apr 27 17:29 drafts  
-rw-rw-rw- 1 researcher2 research_team   46 Apr 27 17:29 project_k.txt  
-rw-r----- 1 researcher2 research_team   46 Apr 27 17:29 project_m.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_r.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_t.txt  

## Change file permissions <a name="permissions">
Check whether any files in the projects directory have write permissions for the owner type of other.

>researcher2@e587efd88d96:~/projects$ `ls -l`  
total 20  
drwx--x--- 2 researcher2 research_team 4096 Apr 27 17:29 drafts  
`-rw-rw-rw-` `1 researcher2 research_team   46 Apr 27 17:29 project_k.txt`  
-rw-r----- 1 researcher2 research_team   46 Apr 27 17:29 project_m.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_r.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_t.txt

We can see that the file `project_k.txt` has write permissions for the owner type of other.  
Change the permissions of the file identified in the previous step so that the owner type of other doesn’t have write permissions using the `chmod` command.
* The `chmod` command `u` sets the permissions for the user who owns the file, `g` sets the permissions for the group that owns the file, and `o` sets the permissions for others.
* Adding `-` (subtract) and/or `+` (add) with `r` (read), `w` (write), and/or `x` (execute) after will add or subtract that permission from user, group, and or other. 
* `chmod o-w project_k.txt`

There will be no output to indicate that the change has been made. To see if the change has been made we will use the `ls -l` command again

>researcher2@e587efd88d96:/projects$ `chmod o-w project_k.txt`   
researcher2@e587efd88d96:/projects$ `ls -l`  
total 20  
drwx--x--- 2 researcher2 research_team 4096 Apr 27 17:29 drafts  
`-rw-rw-r--` `1 researcher2 research_team   46 Apr 27 17:29 project_k.txt`  
-rw-r----- 1 researcher2 research_team   46 Apr 27 17:29 project_m.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_r.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_t.txt 

As seen above the file `project_m.txt` is a restricted file and should not be readable or writable by the group or other; only the user should have these permissions on this file.

>`-rw-r-----` `1 researcher2 research_team   46 Apr 27 17:29 project_m.txt`

Useing the `chmod` command we can change permissions of the `project_m.txt` file so that the group doesn’t have read or write permissions.
* `chmod g-rw project_m.txt`

>researcher2@e587efd88d96:~/projects$ `chmod g-rw project_m.txt`  
researcher2@e587efd88d96:/projects$ `ls -la`  
total 32  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 17:29 .  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 18:01 ..  
-rw--w---- 1 researcher2 research_team   46 Apr 27 17:29 .project_x.txt  
drwx--x--- 2 researcher2 research_team 4096 Apr 27 17:29 drafts  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_k.txt  
`-rw-------` `1 researcher2 research_team   46 Apr 27 17:29 project_m.txt`  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_r.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_t.txt  

## Change file permissions on a hidden file <a name="permissions2">
As mentioned above we can see any hidden files if we add the `-a` modifier and combine it with the `-l` modifier when using the `ls` command.  
* `ls -a`

>researcher2@e587efd88d96:~/projects$ `chmod g-rw project_m.txt`  
researcher2@e587efd88d96:/projects$ `ls -la`  
total 32  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 17:29 .  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 18:01 ..  
`-rw--w---- 1 researcher2 research_team   46 Apr 27 17:29` `.project_x.txt`  
drwx--x--- 2 researcher2 research_team 4096 Apr 27 17:29 drafts  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_k.txt  
-rw------- 1 researcher2 research_team   46 Apr 27 17:29 project_m.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_r.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_t.txt

In most Linux file managers, hidden files and directories start with a dot `.` prefix, such as `.bashrc` or `.config.`

The file `.project_x.txt` is a hidden file that has been archived and should not be written to by anyone. (The user and group should still be able to read this file.)

>`-rw--w---- 1 researcher2 research_team   46 Apr 27 17:29` `.project_x.txt`  

Currently both the User and Group have write permissions. To fix this we will use the `chmod` command again.
* `chmod ug-w .project_x.txt`

>researcher2@e587efd88d96:/projects$ `chmod ug+r-w .project_x.txt`  
researcher2@e587efd88d96:/projects$ `ls -la`  
total 32  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 17:29 .  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 18:01 ..  
`-r--r----- 1 researcher2 research_team   46 Apr 27 17:29 .project_x.txt`  
drwx--x--- 2 researcher2 research_team 4096 Apr 27 17:29 drafts  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_k.txt  
-rw------- 1 researcher2 research_team   46 Apr 27 17:29 project_m.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_r.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 17:29 project_t.txt  

## Change directory permissions <a name="permissions3">
Only the `researcher2` user should be allowed to access the `drafts` directory and its contents. (This means that only `researcher2` should have execute privileges.)  
As we can see from the output, the `u` (user), `researcher2`, and `g` (group), `research_team`, have access to the `drafts` directory.  
>`drwx--x---` `2 researcher2 research_team` `4096 Apr 27 17:29 drafts`  

To remove the execute permission for the group from the drafts directory. We will use the `chmod` command again.
* `chmod g-x drafts`

>researcher2@2dfe8e5aabad:/projects$ `chmod g-x drafts`              
researcher2@2dfe8e5aabad:~/projects$ `ls -la`  
total 32  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 18:09 .  
drwxr-xr-x 3 researcher2 research_team 4096 Apr 27 19:01 ..  
-r--r----- 1 researcher2 research_team   46 Apr 27 18:09 .project_x.txt  
`drwx------` `2 researcher2 research_team 4096 Apr 27 18:09 drafts`  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 18:09 project_k.txt  
-rw------- 1 researcher2 research_team   46 Apr 27 18:09 project_m.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 18:09 project_r.txt  
-rw-rw-r-- 1 researcher2 research_team   46 Apr 27 18:09 project_t.txt  

## Summary <a name="summary">
With that, we now understand how to navigate through a Linux directory and manage file permissions.
