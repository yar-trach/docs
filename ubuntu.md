# LAUNCH SUBLIME TEXT 3 FROM THE COMMAND LINE

> Enter this code in Command prompt to be able to run commands with other name "sub"

```console
sudo ln -s /opt/sublime_text/sublime_text /usr/local/bin/sub
```




# CHANGE USER PASSWORD FROM TERMINAL (SHORT PASS)

>Edit */etc/pam.d/common-password* (change *minlen* to 1 and remove *obscure*):

```text
password    [success=1 default=ignore]  pam_unix.so minlen=1 sha512
```

>type

```console
sudo passwd username
```
