# Display processes

## ps command

`ps [OPTIONS]`

Report a snapshot of the current processes

`ps aux` <> `ps -aux`. If system don't have user x then `ps aux` ~ `ps -aux`. It'll display all process of system.

```
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.5  0.3 168156 11496 ?        Ss   15:37   0:08 /sbin/init maybe-ubiquity
root           2  0.0  0.0      0     0 ?        S    15:37   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   15:37   0:00 [rcu_gp]
root           4  0.0  0.0      0     0 ?        I<   15:37   0:00 [rcu_par_gp]
root           9  0.0  0.0      0     0 ?        I<   15:37   0:00 [mm_percpu_wq]
root          10  0.0  0.0      0     0 ?        S    15:37   0:00 [ksoftirqd/0]
root          11  0.1  0.0      0     0 ?        I    15:37   0:03 [rcu_sched]
hiepdx23    1187  0.0  0.1 169516  3384 ?        S    15:37   0:00 (sd-pam)
hiepdx23    1303  0.1  0.2  13932  6240 ?        S    15:37   0:02 sshd: hiepdx23@pts/0
hiepdx23    1304  0.0  0.1   8800  5812 pts/0    Ss   15:37   0:00 -bash
root        1482  0.0  0.0      0     0 ?        I    15:42   0:00 [kworker u256:1-events_power_efficient]
root        1493  0.0  0.0      0     0 ?        I    15:42   0:00 [kworker/1:0]
root        2423  0.2  0.0      0     0 ?        I    15:52   0:02 [kworker/0:0-events]
root        2462  0.0  0.0      0     0 ?        I    15:54   0:00 [kworkeru256:0-events_unbound]
root        2614  0.0  0.0      0     0 ?        I    15:59   0:00 [kworkeru256:2-events_unbound]
hiepdx23    2846  0.0  0.1   8888  3236 pts/0    R+   16:06   0:00 ps aux
```

If we use command `ps -au"user-name"` ex `ps -auhiepdx23`

Result:
```
PID TTY          TIME CMD
1186 ?        00:00:00 systemd
1187 ?        00:00:00 (sd-pam)
1303 ?        00:00:02 sshd
1304 pts/0    00:00:00 bash
2903 pts/0    00:00:00 ps
``` 

Some popular options of `ps`

```
To print a process tree:
    ps -ejH
    ps axjf
    
To get info about threads:
    ps -eLf
    ps axms

To get security info:
    ps -eo euser,ruser,suser,fuser,f,comm,label
    ps axZ
    ps -eM

To see every process running as root (real & effective ID) in user format:
    ps -U root -u root u

To see every process with a user-defined format:
    ps -eo pid,tid,class,rtprio,ni,pri,psr,pcpu,stat,wchan:14,comm
    ps axo stat,euid,ruid,tty,tpgid,sess,pgrp,ppid,pid,pcpu,comm
    ps -Ao pid,tt,user,fname,tmout,f,wchan
```
