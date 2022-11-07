# I. User Managament

## 1. File Configure

Entire basic information of user is in **/etc/passwd** file. Normal user have UID above 1000. System user have UID from 100 to 999

Entire basic information of group is in **/etc/group** file.

In **/etc/shadow** file, it containts some information of user: encoded password, last password change, ...

File **/etc/skel** will be copied to **home** director of new user when we add a new user.

## 2. Command

`adduser` 
Adding a new user. This command has some options. We can modify file configuration at **/etc/adduser.conf**. Ex: We can change bash from **/bin/bash** -> **/bin/sh**

Ex: we can change current home directory when using **adduser --home**

`deluser`
Deleting a user.

`addgroup` 
Adding a new gorup.

`delgroup`
Deleting a group.

`usermod`
Modifying information of user. Ex: we can change current home directory of a user, GID, UID,... We also can lock a user account. When lock user by password, we'll see "!" charactor at password field in **/etc/shadow** file. Beside we can also protect a account when putting shell is **/bash/false** or putting expiration date.

`groupmod`
Modifying information of group. Ex: we can change GID, ...

`passwd`
Changing user password. We also use this command to lock user account.




