Sticky bits are a type of file permission in Linux that can be set on directories. This type of permission provides an extra layer of security when controlling the deletion and renaming of files within a directory. It is typically used on directories that are shared by multiple users to prevent one user from accidentally deleting or renaming files that are important to others.

For example, in a shared home directory, where multiple users have access to the same directory, a system administrator can set the sticky bit on the directory to ensure that only the owner of the file, the owner of the directory, or the root user can delete or rename files within the directory. This means that other users cannot delete or rename files within the directory as they do not have the required permissions. This provides an added layer of security to protect important files, as only those with the necessary access can delete or rename files. Setting the sticky bit on a directory ensures that only the owner, the directory owner, or the root user can change the files within the directory.

When a sticky bit is set on a directory, it is represented by the letter “`t`" in the execute permission of the directory's permissions. For example, if a directory has permissions “`rwxrwxrwt`", it means that the sticky bit is set, giving the extra level of security so that no one other than the owner or root user can delete or rename the files or folders in the directory.

Permission Management

```shell-session
cry0l1t3@htb[/htb]$ ls -l

drw-rw-r-t 3 cry0l1t3 cry0l1t3   4096 Jan 12 12:30 scripts
drw-rw-r-T 3 cry0l1t3 cry0l1t3   4096 Jan 12 12:32 reports
```

In this example, we see that both directories have the sticky bit set. However, the `reports` folder has an uppercase `T`, and the `scripts` folder has a lowercase `t`.

If the sticky bit is capitalized (`T`), then this means that all other users do not have `execute` (`x`) permissions and, therefore, cannot see the contents of the folder nor run any programs from it. The lowercase sticky bit (`t`) is the sticky bit where the `execute` (`x`) permissions have been set.