# Options

```shell
find path -name "name" # Search by name
```

```shell
find path -iname "name" # Search by name whithout import uppercase or lowercase
```

```shell
find path -type <f> "file" # Search by file
find path -type <d> "directory" # Search by directory
find path -type <l> "link" # Search by links
find path -type <b> "blocks" # Search by  block advisers
find path -type <l> "character" # Search by character advisers
find path -type <p> "link" # Search by pipes
find path -type <s> "socket" # Search by sockets
```

```shell
find path -size [+/-]n(c, K, M, G) # Search by size grather than or lower than
	number  # Blocks equals 512 bytes
	c # Search in Bytes
	K # Search in Kilo bytes
	M # Search in Mega bytes
	G # Search in Giga bytes
```

```shell
find path -perm -num or +num # Search by permissions in number format equals to
find path -perm /num # Search by permissions in number format at least
```

```shell
find path -user "user" # Search by user
```

```shell
find path -group "group" # Search by group
```

```shell
find path -mmin [+/-]n # Search by files modifies since n minutes
```

```shell
find path -mtime [+/-]n # Search by files modifies since n days
```

```shell
find path -maxdepth n -search "name" # Redefine descending the search to n paths
```

```shell
find path -iname "*.conf*" -exec cp '{}' destination ';' # Look for .conf files in the path and copy them to the destination
```