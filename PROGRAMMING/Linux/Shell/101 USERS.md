#### Create user
```shell
adduser user_name
```

#### Create groups
```shell
addgroup user_name
```

#### Assign groups
```shell
usermode -g group user_name
```

#### Change the user file
```shell
chown user file_name
```

#### Change the group file and the user file
```shell
chown user:group file_name
```

#### Change the group file
```shell
chown :group file_name
```

#### Change password
```shell
passwd # Change current user password
```
```shell
passwd user # Change user_name password
```

#### Change Permisions
```shell
chmod +r file_name # Give all read permisions (user-group-others)
chmod -r file_name # Quit all read permisions (user-group-others)
```
```shell
chmod u+r file_name # Give the user read permisions
chmod u=r file_name

chmod u-r file_name # Quit the user read permisions
chmod u=wx file_name

chmod g+w file_name # Give the group write permisions
chmod g=w file_name

chmod g-r file_name # Quit the group read permisions
chmod g=wx file_name

chmod o+x file_name # Give the other groups execution permisions
chmod o=x file_name 

chmod o-r file_name # Quit the other groups read permisions
chmod o=wx file_name 

chmod o-r,g+x,u+r file_name # Combine
chmod u=,g=,o= file_name # Quit all permissions
chmod u=rwx,g=rwx,o=rwx file_name # Give all permissions
```

#### Permissions with binaries
| R  | W   | X    |R  | W   | X    |R  | W   | X    |
| --- | --- | --- |--- | --- | --- |--- | --- | --- |
| 1   | 1   |  1  |  1 | 1   |  1  |  1 |  1  |  1  |
```shell
rw-  r--  ---
110  100  000
6     4    0 => Exagesimal
chmod 640 file_name # Give all read permisions (user-group-others)
```
| Binario | Octal  |
| ---     | ---    |
| 000     |    0   |
|001      |    1   |
|010      |    2   |
|011      |    3   |
|100      |    4   |
|101      |    5   |
|110      |    6   |
|111      |    7   |
