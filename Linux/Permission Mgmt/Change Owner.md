


To change the owner and/or the group assignments of a file or directory, we can use the `chown` command. The syntax is like following:

#### Syntax - chown

Permission Management

```shell-session
cry0l1t3@htb[/htb]$ chown <user>:<group> <file/directory>
```

In this example, "shell" can be replaced with any arbitrary file or folder.

Permission Management

```shell-session
cry0l1t3@htb[/htb]$ chown root:root shell && ls -l shell

-rwxr-xr--   1 root root 0 May  4 22:12 shell
```
