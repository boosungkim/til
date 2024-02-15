# How to handle unsafe gpg directories

When I was creating a new gpg directory in my new home partition, I got this warning:

```bash
gpg: WARNING: unsafe permissions on homedir '/home/boosung/.gnupg'
```

To resolve this warning, I simply ran `chmod 700 .gnupg/`.

7 indicates that the user has read, write, and execute permissions. The first 0 indicates that the group has no permissions. The second 0 indicates that other users have no permissions either.