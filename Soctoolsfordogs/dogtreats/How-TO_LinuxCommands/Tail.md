## Tail Command
[tail](https://www.linode.com/docs/guides/how-to-use-tail/)

To run log, last 10 lines:
```
tail /var/log/auth.log
```

To run with specified num of lines:
```
tail -n 50 /var/log/auth.log
```

To run dynamically, as file changes:
```
tail -f /var/log/auth.log
```

Run and filter with [[Grep]]:
```
tail /var/log/auth.log | grep 198.51.100.1
```

#howto_linux_commands