# I. User Managament

## 1. Configuration File

### 1.1 User
Configuration file of user is **/etc/passswd** file

```
root:!:0:0::/:/usr/bin/ksh
daemon:!:1:1::/etc:
bin:!:2:2::/bin:
sys:!:3:3::/usr/sys: 
adm:!:4:4::/var/adm:
uucp:!:5:5::/usr/lib/uucp: 
guest:!:100:100::/home/guest:
nobody:!:4294967294:4294967294::/:
lpd:!:9:4294967294::/:
lp:*:11:11::/var/spool/lp:/bin/false 
invscout:*:200:1::/var/adm/invscout:/usr/bin/ksh
nuucp:*:6:5:uucp login user:/var/spool/uucppublic:/usr/sbin/uucp/uucico
paul:!:201:1::/home/paul:/usr/bin/sh
jdoe:*:202:1:John Doe:/home/jdoe:/usr/bin/bash
```

**/etc/passwd** file has seven fields:

- User name

- Encrypted password

- User ID number (UID)

- User's group ID number (GID)

- Full name of the user (GECOS)

- User home directory

- Login shell

Normal user have UID above 1000. System user have UID from 100 to 999

### 1.2 Group

Configuration file of user is **/etc/group** file.

```
staff:x:1:shadow,cjf
employee:!:1000:hiepdx23
```
**/etc/group** file has four fields:

- Group name

- Encrypted password

- Group ID number (GID)

- Users of group

### 1.3 Some infomation of user

Configuration file abour information of user is **/etc/group** file. It contain some information about account user as encrypt password, date of last password change, minimum required days between password changes, maximum allowed days between password changes, ...

### 1.4 /etc/skel

File **/etc/skel** will be copied to **home** director of new user when we add a new user.

## 2. Command

### 2.1 Add user and group

`adduser` 
Adding a new user. This command has some options. We can modify file configuration at **/etc/adduser.conf**. Ex: We can change bash from **/bin/bash** -> **/bin/sh**

`addgroup` 
Adding a new gorup.

Ex: we can change current home directory when using **adduser --home**

### 2.2 Delete user and group

`deluser`
Deleting a user.


`delgroup`
Deleting a group.

### 2.3 Modify user and group

`usermod`
Modifying information of user. Ex: we can change current home directory of a user, GID, UID,... We also can lock a user account. When lock user by password, we'll see "!" charactor at password field in **/etc/shadow** file. Beside we can also protect a account when putting shell is **/bash/false** or putting expiration date.

`groupmod`
Modifying information of group. Ex: we can change GID, ...

`passwd`
Changing user password. We also use this command to lock user account.

### 2.4 Add and remove user to group

`gpasswd` command and `usermod` command is used to add a user to group.

`deluser [user] [group]` command is used to remove a user to group.

# II. Permission

Permission is a attribute of a folder and file. Normally, there are three basic permission is **reade**, **write** and **execute**. 

In linux, three type of user (owner, group, other) can use file and folder. At permission field of file and folder, it has 9 bits to represent permission of three type of user (ex: 110110111 = rw-rw-rwx). First three bits represent permission of **owner**, next represent **group**, end represent **other**.

## 1.Command

### 1.1 View permission

Basic command to view permission file or folder

`ls -l name_file or name_folfer` 

result:

```
drwxrwsr-x 4294967295 hiepdx employee 2147549184 Sep 2 17:01 job
-rwxrwsr-x 4294967295 hiepdx employee 2147549184 Sep 2 17:01 job
```

Advance command to view permission file or folder

`getfacl name_file or name_folfer`

result:

```
# file: mydir

# owner: quanta

# group: quanta

user::rwx

user:kitty:rwx                  #effective:r-x

group::r-x

group:friends:rwx               #effective:r-x

mask::r-x

other::---

default:user::rwx

default:group::r-x

default:group:friends:r-x

default:mask::r-x

default:other::---
```

**mask** infomation above respresent maximum permission that different user and group may have it. As above, **user: kitty** and **group: friend** have **rwx** permission but **mask** have infomation is **r-x**. Therefore, **user: kitty** and **group: friend** just have **read and execute** permission (it is represented by **#effective:r-x**).

**default** informations will be added when we create sub-folder of root-folder. When we create sub-file, informations of **default:user** and **default:group** will be added to permission of sub-file. Default **mask** and **other** information of file is **r--**. 

### 1.2 Modify permission

`drwxrwsr-x 4294967295 hiepdx employee 2147549184 Sep 2 17:01 job`

When we want modify permission of user, group and other is written in third and fourth filed (hiepdx employee), we use:

`chmod`

Having a advance command to modify permission of file and folder is:

`setfacl [option] name_file or name_folder`

Some option of setfacl:

`setfacl -m ...` add acls <> `setfal -x g:g1 file_name` delete acl of group **g1**.
`setfacl -b ...` remove all acls.`