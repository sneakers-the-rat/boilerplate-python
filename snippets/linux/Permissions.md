Also see [[chmod]]

## [[Users]] and [[Groups]]

### Create new Group
```groupadd <groupname>```

### Create new User
```useradd <username>```
Create a new user and add to primary group `users` and other groups
`useradd -g users -G <group1>,<group2> <username>`

### Add user to group
```usermod -a -G <group1>,<group2> <username>```
** important! don't forget the `-a` or you will remove them from all the other groups they are in!

### Show Groups
`getent group`

### Show members of a group
```getent group <groupname>```


