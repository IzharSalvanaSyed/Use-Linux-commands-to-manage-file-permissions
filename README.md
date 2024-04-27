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
displays the file structure of the `/home/researcher2/projects` directory
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

![image](https://github.com/IzharSalvanaSyed/Use-Linux-commands-to-manage-file-permissions/assets/156041933/19fd024c-12fb-42e1-99a8-925af0cfbfe5)

Navigate to the `projects` directory. 
* `cd projects`

![image](https://github.com/IzharSalvanaSyed/Use-Linux-commands-to-manage-file-permissions/assets/156041933/22d3af9c-f9b9-40fe-886c-986c6916fdf9)

List the contents and permissions of the `projects` directory.
* To list out the contents of the directory, use the same command as above but add a modifier to give the contents of the directories permissions
* `ls -l`

![image](https://github.com/IzharSalvanaSyed/Use-Linux-commands-to-manage-file-permissions/assets/156041933/d8abc7c4-0dd9-46d1-a1f2-c08d43d09931)

If we use the `ls` without the `-l` modifier, we are presented with:
![image](https://github.com/IzharSalvanaSyed/Use-Linux-commands-to-manage-file-permissions/assets/156041933/1d74e277-a380-4173-ae30-642fd823741b)

As you can see above, it lists the same contents within the directory with less information. We must look at one of them to understand what the `-l` modifier provides.

`drwx--x--- 2 researcher2 research_team 4096 Apr 27 16:40 drafts`

* The 1st character indicates the file type. The `d` indicates it’s a directory. When this character is a hyphen `-`, it's a regular file.
* The 2nd-4th characters indicate the read `r`, write `w`, and execute `x` permissions for the user. When one of these characters is a hyphen `-` instead, it indicates that this permission is not granted to the user.
* The 5th-7th characters indicate the read `r`, write `w`, and execute `x` permissions for the group. When one of these characters is a hyphen `-` instead, it indicates that this permission is not granted for the group.
* The 8th-10th characters indicate the read `r`, write `w`, and execute `x` permissions for the owner type of other. This owner type consists of all other users on the system apart from the user and the group. When one of these characters is a hyphen `-` instead, that indicates that this permission is not granted for other.
