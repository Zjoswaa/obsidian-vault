Files with the SUID bit set will be run with permissions of the file owner, this can be used to run certain files you otherwise wouldnt be able to.

To find all files on the system with the bit set:
```bash
find / -perm -u=s -type f 2>/dev/null
```
> [!info]
> `2>/dev/null` surpresses any errors.
