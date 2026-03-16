# minimal-proc-monitor-in-C

Small Linux process scanner written in C.

The program reads information about running processes directly from the `/proc` filesystem and displays basic statistics such as:

* PID
* User
* Process state
* CPU usage
* Memory usage
* Process name

## Features

* Reads data directly from `/proc`
* No external dependencies
* Simple and lightweight
* Demonstrates low-level Linux process inspection

## Build

```bash
gcc src/procinfo.c -o procinfo
```

or using Makefile:

```bash
make
```

## Usage

```bash
./procinfo
```

Example output:

```
PID      USER   ST CPU%     MEM(KB)    NAME
-------------------------------------------
1        root   S  0.00     1234       systemd
234      user   R  0.21     4212       bash
812      user   S  1.32     8340       firefox
```

## How it works

The program reads data from:

* `/proc/[pid]/stat`
* `/proc/[pid]/statm`
* `/proc/[pid]/status`
* `/proc/[pid]/comm`

It parses these files manually to extract:

* CPU time (`utime`, `stime`)
* memory usage (RSS)
* process state
* UID
* process name

CPU usage is calculated by sampling process CPU time twice with a short delay.

## Requirements

* Linux
* GCC
* `/proc` filesystem

## License

MIT
