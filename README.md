# check_diskstats
A standalone version of the openATTIC check_diskstats Nagios Plugin to monitor disk I/O, request size, disk load, and more.

### Features
- Optional Disk Argument: Monitor a specific disk (e.g., sda) or omit the argument to automatically discover and monitor all physical disks.
- Nagios Compliant: Correct multi-device output formatting and performance data (perfdata) for graphing tools like Grafana or PNP4Nagios.
- State Persistence: Uses /dev/shm to store temporary state files for accurate interval calculation.

## How to use
The script requires write access to /dev/shm/ to store state information between checks.

````
# Optional: Ensure the script is executable
chmod +x check_diskstats

# Monitor a specific disk
./check_diskstats sda

# Monitor all disks (Auto-Discovery)
./check_diskstats
````

## Nagios Configuration

Command Definition
````
define command {
    command_name    check_diskstats
    command_line    $USER1$/check_diskstats -w $ARG1$ -c $ARG2$ $ARG3$
}
````

Service Definition (Specific Disk)
````
define service {
    ...
    check_command   check_diskstats!75!85!sda
}
````

Service Definition (All Disks)
````
define service {
    ...
    check_command   check_diskstats!70!90
}
````

### Output Examples
Single Disk
````
sda: OK (2.29%) | sda_util=2.29%;75;85;0;100 sda_rd_iops=18.52 sda_wr_iops=192.21 sda_rd_bps=169288.34B sda_wr_bps=6569377.97B
````

All Disks (Auto-Discovery)
````
sda: OK (1.15%), sdb: WARNING (78.40%), sr0: OK (0.00%) | sda_util=1.15%;75;85;0;100 ... sdb_util=78.40%;75;85;0;100 ...
````

## License
````
Copyright (C) 2011-2026, AVENDIS GmbH
Copyright (c) 2017 SUSE LLC
Copyright (c) 2024-2026 (Modifications for multi-disk support)

openATTIC is free software; you can redistribute it and/or modify it
under the terms of the GNU General Public License as published by
the Free Software Foundation; version 2.

This package is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.
````
