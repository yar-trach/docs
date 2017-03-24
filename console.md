# PID - task ID in console

> * pid
> * tasks
> * search

Write it in console to find Grunt's PID 

```console
ps aux | grep grunt
```

Find in table 'grunt' and it PID,
Write it in console to kill Grunt task

```
kill <pid>
```





# Find and connect to Bluetooth device

>* bluetooth
>* ueboom
>* speaker

Problem with connecting to BT speaker UEBOOM
Run in terminal "sdptool browse <MAC address>"
UEBOOM MAC is 88:C6:26:07:3F:3C

```console
sdptool browse 88:C6:26:07:3F:3C
```

After this you should see text about browsing

Browsing 88:C6:26:07:3F:3C ...


