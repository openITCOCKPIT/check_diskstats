
# check_diskstats

A standalone version of the [openATTIC check_diskstats](https://bitbucket.org/openattic/openattic/) Naemon/Nagios plugin for monitoring Linux disk I/O and utilization.

## Features

- Collects and reports detailed disk statistics on Linux systems
- Calculates disk load as a percentage (utilization)
- Reports IOPS (read/write/total), normalized IOPS, and request size
- Measures average I/O wait times and service times
- Outputs read/write throughput (bytes per second)
- Supports configurable warning and critical thresholds for disk load
- Designed for integration with openITCOCKPIT, Naemon or Nagios
- Outputs performance data for monitoring systems

## What is it used for?

This plugin is used to monitor the performance and health of block devices (disks) on Linux systems. It provides detailed metrics such as disk load, IOPS, request size, and I/O wait times, which are essential for identifying disk bottlenecks, diagnosing performance issues, and alerting when disk utilization exceeds defined thresholds. It is suitable for use in monitoring environments like openITCOCKPIT, Naemon or Nagios.

This plugin requires Python 3.


## How to use

```sh
chmod +x check_diskstats
./check_diskstats /dev/sda
```


### Example Nagios Command

```nagios
define command{
    command_name                        check_diskstats
    command_line                        $USER1$/check_diskstats $ARG1$
}

define command{
    command_name                        check_diskstats_with_args
    command_line                        $USER1$/check_diskstats $ARG1$ --warning $ARG2$ --critical $ARG3$
}
```


### Output Example

```
Ok: Disk load for sda is at 2.29%.|rd_iops=18.52 wr_iops=192.21 tot_iops=210.73 rd_normiops=41.33 wr_normiops=1603.85 tot_normiops=1645.18 rd_normratio=2.23 wr_normratio=8.34 rd_bps=169288.34B/s wr_bps=6569377.97B/s tot_avg_wait=0.000150s rd_avg_wait=0.000198s wr_avg_wait=0.000146s rd_avg_size=9141.07B wr_avg_size=34178.16B load_percent=2.29%;75;85;0;100 ioindex=92 normindex=719
```


### Options
Run `./check_diskstats --help` for a full list of available options and usage information.

# License
```
Copyright (C) 2011-2012, it-novum GmbH
Copyright (c) 2017 SUSE LLC
Copyright (c) 2025-today AVENDIS GmbH
 
openATTIC is free software; you can redistribute it and/or modify it
under the terms of the GNU General Public License as published by
the Free Software Foundation; version 2.

This package is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.
```
