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

## top command

`top`

Display processes that have dynamic state - not snapshot

```
top - 16:17:48 up 40 min,  1 user,  load average: 0.09, 0.05, 0.01
Tasks: 219 total,   1 running, 218 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.1 sy,  0.0 ni, 99.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   2957.5 total,   2277.6 free,    293.3 used,    386.7 buff/cache
MiB Swap:   1957.0 total,   1957.0 free,      0.0 used.   2497.4 avail Mem

PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
    1 root      20   0  168156  11496   8484 S   0.3   0.4   0:08.71 systemd
    11 root      20   0       0      0      0 I   0.3   0.0   0:04.65 rcu_sched
2423 root      20   0       0      0      0 I   0.3   0.0   0:04.42 kworker/0:0-events
2883 root      20   0       0      0      0 I   0.3   0.0   0:00.38 kworker/u256:1-events_power_efficient
3083 hiepdx23  20   0    9372   3976   3180 R   0.3   0.1   0:00.04 top
    2 root      20   0       0      0      0 S   0.0   0.0   0:00.02 kthreadd
    3 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_gp
    4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_par_gp
    6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/0:0H-events_highpri
    8 root       0 -20       0      0      0 I   0.0   0.0   0:01.09 kworker/0:1H-kblockd
    9 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 mm_percpu_wq
    10 root      20   0       0      0      0 S   0.0   0.0   0:00.11 ksoftirqd/0
```

Information of NI (NICE) field tells us about priority of this process (the lower this index, the higher the priority) -20 -> 20.

Infomation of PR field is index of NI filed + 20. 

## Modify processes

We can alter priority of the process by `renice` command.

`renice [-n] priority [-g|-p|-u] identifier...`

example:

`renice -n +2/-2 -p 3504`

The process have pid is 3504 will have new priority: +2/-2

## Kill processes

We can kill the process by `kill` command

`kill [options] <pid> [...]`

example:

`kill 3504`. The process have index: 3504 is killed.

**Note: We have to use kill -9 to kill process carefully because using it many time can creates zombies process. When we use ***kill*** command, it will send SIGTERM, not SIGKILL. Let learn about ***7 signal*** to have more information **

## State of process

```
USER        PID STAT    COMM
hiepdx23    1392 S      systemd
hiepdx23    1393 S      (sd-pam)
hiepdx23    1398 S      bash
hiepdx23    2963 S      sshd
hiepdx23    2964 S      bash
hiepdx23    4531 T      nano
hiepdx23    4606 R      ps
hiepdx23    4607 S      grep
```

We have three main state of user's process is S(sleep) T(stopped) R(running)

- S: Wating for event to complete
- T: Stopped, run `fg` command to run this process
- R: Running
