We can modify permissions using the `chmod` command, permission group references (`u` - owner, `g` - Group, `o` - others, `a` - All users), and either a [`+`] or a [`-`] to add remove the designated permissions. In the following example, let us assume we have a file called `shell` and we want to change permissions for it so this script is owned by that user, becomes not executable, and set with read/write permissions for all users.

Permission Management

```shell-session
cry0l1t3@htb[/htb]$ ls -l shell

-rwxr-x--x   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

We can then apply `read` permissions for all users and see the result.

Permission Management

```shell-session
cry0l1t3@htb[/htb]$ chmod a+r shell && ls -l shell

-rwxr-xr-x   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

We can also set the permissions for all other users to `read` only using the octal value assignment.

Permission Management

```shell-session
cry0l1t3@htb[/htb]$ chmod 754 shell && ls -l shell

-rwxr-xr--   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

Let us look at all the representations associated with it to understand better how the permission assignment is calculated.

Permission Management

```shell-session
Binary Notation:                4 2 1  |  4 2 1  |  4 2 1
----------------------------------------------------------
Binary Representation:          1 1 1  |  1 0 1  |  1 0 0
----------------------------------------------------------
Octal Value:                      7    |    5    |    4
----------------------------------------------------------
Permission Representation:      r w x  |  r - x  |  r - -
```

If we sum the set bits from the `Binary Representation` assigned to the values from `Binary Notation` together, we get the `Octal Value`. The `Permission Representation` represents the bits set in the `Binary Representation` by using the three characters, which only recognizes the set permissions easier.