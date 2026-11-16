## Journald

A walkthrough on how the linux system records and keeps logs. The linux Diary

### Introduction

To understand system logging, we'll need to understand the rsyslog service. The rsyslog service is responsible for collecting, sorting and writing the syslogs messages to log files located in the `/var/log` directory. In addition to the syslog messages, the `/var/log` directory contain logs from other services.

#### RsysloG

Rsyslog uses the syslog protocol to implement syslogging. Applications and developers can configure rsyslog with rules to determine how to handlethe logs. These files are drop-in located in the `/etc/rsyslog.d/` directory, these files should also have the `.conf` extension.

These rules are made up of a filter, followed by an action. Filters select a subset of the syslog messages, these filters can be priority/facility based, it is possible to use a wildcard (\*) to match all the possible values. **Actions** indicate how to handle these messages, actions can also include a path to save the messages and an action can be more than one for each rule.

Example: to save any message from the `authpriv` facility in the `/var/log/secure` file, such a rule would be 
```bash
    authpriv.* /var/log/secure 
```
It is possible to specify a priority for a rule; all messages of that facility of that priority will be saved to the action. 
Example: To save all messages from the `authpriv` facility with the `warning` priority to `/var/log/secure`, the rule will be 

```bash
    authpriv.warning /var/log/secure
```

##### Key
- **Facility** : THe source or component that geberated a system message; origin of a message 

#### Log rotation
Log rotation is needed to prevent the log files from taking up alot of disk space in a system. The system does this by running the `logrotate` command, this is periodically triggered by a system unit, [read about system units here](https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files).  

After approximately 4 weeks, the earliest log files are deleted to reclaim disk space, log files are saved according to this format `/var/log/messages-YYYMMDD`. After the log file is rotated, a new log file is created and the log files' associated system is notified.

Logrotate command rotates logs according to configurations or when a log file reaches a certain size.

#### Sending logs manually 
To send logs manually, the `logger` command is used, it sends alerts to the rsyslog service. It sends the user type and priority of the message.

### Finding Events in the system-journal
The system uses the systemd-journald service to log events, it logs events in an indexed binary file known as a journal. It also contains metadata about the log event.

To retrieve messages from the journal, we use the `journalctl` command. Running this command as the root user, it shows all the messages as compared to a normal user whose output is limited. The output is also color-coded; notice and warning priority messages in bold, while error priority or higher are in red.

#### Journalctl options

Journalctl supports varioius options depending on what you want to see. 

- To see n number of lines, you can run 

```bash
    journalctl -n 5
    
    Nov 16 11:01:01 kofianyekundu CROND[10330]: (root) CMD (run-parts /etc/cron.hourly)
    Nov 16 11:01:01 kofianyekundu run-parts[10333]: (/etc/cron.hourly) starting 0anacron
    Nov 16 11:01:01 kofianyekundu run-parts[10339]: (/etc/cron.hourly) finished 0anacron
    Nov 16 11:01:01 kofianyekundu CROND[10329]: (root) CMDEND (run-parts /etc/cron.hourly)

```
- Journalctl also supports following, like the tail command. To follow output, continiously, you run the command with the -f option.

```bash 
    journalctl -f 
    Nov 16 10:46:01 kofianyekundu systemd[1]: Starting fwupd-refresh.service - Refresh fwupd metadata and update motd...
    Nov 16 10:46:01 kofianyekundu systemd[1]: fwupd-refresh.service: Deactivated successfully.
    Nov 16 10:46:01 kofianyekundu systemd[1]: Finished fwupd-refresh.service - Refresh fwupd metadata and update motd.
    Nov 16 10:54:56 kofianyekundu wpa_supplicant[1494]: wlo1: CTRL-EVENT-BEACON-LOSS
    Nov 16 10:57:21 kofianyekundu wpa_supplicant[1494]: wlo1: RSN: Group rekeying completed with 48:bf:74:3c:28:17 [GTK=CCMP]
    Nov 16 11:01:01 kofianyekundu CROND[10330]: (root) CMD (run-parts /etc/cron.hourly)
    Nov 16 11:01:01 kofianyekundu run-parts[10333]: (/etc/cron.hourly) starting 0anacron
    Nov 16 11:01:01 kofianyekundu run-parts[10339]: (/etc/cron.hourly) finished 0anacron
    Nov 16 11:01:01 kofianyekundu CROND[10329]: (root) CMDEND (run-parts /etc/cron.hourly)
```

- To filter output by priority, you run the journalctl command with the -p option and the priority(can be name or number). The journal supports the following levels
- debug
- info 
- notice 
- warning
- err
- crit
- alert
- emerg

```bash 
$ journalctl -p err
Nov 16 12:04:07 kofianyekundu kernel: x86/cpu: SGX disabled or unsupported by BIOS.
Nov 16 12:04:07 kofianyekundu kernel: ACPI BIOS Error (bug): Could not resolve symbol [\_SB.PCI0.DGPV], AE_NOT_FOUND (20240827/psargs-332)
Nov 16 12:04:07 kofianyekundu kernel: ACPI Error: Aborting method \_SB.PCI0.RP05.PCRP._ON due to previous error (AE_NOT_FOUND) (20240827/psparse-529)
Nov 16 12:04:08 kofianyekundu kernel: Warning: Unmaintained driver is detected: cnic
Nov 16 12:04:08 kofianyekundu kernel: Warning: Unmaintained driver is detected: cnic_init
Nov 16 12:04:08 kofianyekundu kernel: Warning: Unmaintained driver is detected: bnx2i
Nov 16 12:04:08 kofianyekundu kernel: Warning: Unmaintained driver is detected: bnx2i_mod_init
Nov 16 09:04:13 kofianyekundu bluetoothd[1293]: Failed to set mode: Failed (0x03)
Nov 16 09:05:15 kofianyekundu gdm-password][3175]: gkr-pam: unable to locate daemon control file
```
*alerts of type err will be red in color*

- To filter messages from a particular unit, you can use the -u option

```bash 
journalctl -u sshd.service

Nov 16 09:04:14 kofianyekundu systemd[1]: Starting sshd.service - OpenSSH server daemon...
Nov 16 09:04:14 kofianyekundu sshd[1510]: Server listening on 0.0.0.0 port 22.
Nov 16 09:04:14 kofianyekundu sshd[1510]: Server listening on :: port 22.
Nov 16 09:04:14 kofianyekundu systemd[1]: Started sshd.service - OpenSSH server daemon.

```

- Journalctl also supports filterig output by certain time range, by using the `--since` and `--until` options. The time ranges can take time arguments such as today, yesterday and tomorrow, these are considered valid. But if you want to specify time, it takes the *"YYYY-MM-DD hh:mm:ss"* format. the space is preserved to separate the date and time formats, ideally you can supply either the date or time alone.

Example:
To view today's logs, you can simply run 

```bash
$ journalctl --since today

Nov 16 10:01:02 kofianyekundu anacron[8028]: Anacron started on 2026-11-16
Nov 16 10:01:02 kofianyekundu anacron[8028]: Will run job `cron.daily' in 24 min.
Nov 16 10:01:02 kofianyekundu anacron[8028]: Jobs will be executed sequentially
Nov 16 10:01:02 kofianyekundu run-parts[8030]: (/etc/cron.hourly) finished 0anacron
Nov 16 10:01:02 kofianyekundu CROND[8014]: (root) CMDEND (run-parts /etc/cron.hourly)
Nov 16 10:01:23 kofianyekundu systemd[1]: Starting plocate-updatedb.service - Update the plocate database...
Nov 16 10:01:25 kofianyekundu systemd[1]: plocate-updatedb.service: Deactivated successfully.
Nov 16 10:01:25 kofianyekundu systemd[1]: Finished plocate-updatedb.service - Update the plocate database.
Nov 16 10:01:25 kofianyekundu systemd[1]: plocate-updatedb.service: Consumed 1.356s CPU time, 209.4M memory peak.
Nov 16 10:02:13 kofianyekundu org.mozilla.firefox.desktop[4507]: Safe Browsing server returned a 400 during update:request url = https://safebrowsin>
Nov 16 10:03:41 kofianyekundu cupsd[1507]: REQUEST localhost - - "POST / HTTP/1.1" 200 183 Renew-Subscription successful-ok
Nov 16 10:08:03 kofianyekundu chronyd[1300]: Selected source 160.119.216.206 (2.rhel.pool.ntp.org)
Nov 16 10:22:54 kofianyekundu chronyd[1300]: Selected source 162.159.200.1 (2.rhel.pool.ntp.org)
Nov 16 10:25:02 kofianyekundu anacron[8028]: Job `cron.daily' started
Nov 16 10:25:02 kofianyekundu run-parts[8747]: (/etc/cron.daily) starting brave-browser
Nov 16 10:25:02 kofianyekundu run-parts[8751]: (/etc/cron.daily) finished brave-browser
Nov 16 10:25:02 kofianyekundu run-parts[8753]: (/etc/cron.daily) starting google-chrome
Nov 16 10:25:02 kofianyekundu run-parts[8772]: (/etc/cron.daily) finished google-chrome
Nov 16 10:25:02 kofianyekundu anacron[8028]: Job `cron.daily' terminated
Nov 16 10:25:02 kofianyekundu anacron[8028]: Normal exit (1 job run)

```

to view all journals since 2026-11-12 to 2026-11-14

```bash 
$ journalctl --since 2026-11-12 --until 2026-11-14

*..too long, omitted*
```

To check all entires in the past hr 

```bash

$ journalctl --since "-1 hour"

*....omitted...too long*

```

Other filters include
```bash 
**_COMM** : command name : $ journalctl _COMM=dnf 
**_EXE** : path to executable : $ journalctl _EXE=/usr/bin/dnf
**_PID** : process ID : $ journalctl _PID=2216
**_UID** : user ID : $ journalctl _UID=0
**_SYSTEMD_UNIT** : systemd unit that started the process : $ journalctl _SYSTEMD_UNIT=sshd.service
```   

### Configuring a persistent system journal

By default, the journal files are saved in the `/run/log/journal` directory which is volatile; clears after a system reboot. To configire a persistent one, you can create the `/var/log/journal` directory. If this is done during run time, then it is wise to run `$ journalctl --flush` operation to copy all log files in the volatile dir to the persistent one.
