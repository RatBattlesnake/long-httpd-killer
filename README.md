# long-httpd-killer

## Overview

Sometimes Apache request handler processes can become blocked waiting
on things like NFS, external requests, IO, etc.  This reaper process
is designed to be run either manually, or via cron, to clean things up.

This is a modified version of the original script, written by:

S. Zachariah Sprackett (https://github.com/zsprackett/long-httpd-killer)

The primary goal of this version is to focus on supporting Ubuntu 14.04,
and to target statuses "W" (working), and "G" (gracefully finishing).

## Example Usage

    ./long-httpd-killer -t 60 -s

This command will hit the Apache server status running at 127.0.0.1.
Look for request handlers that have been running for longer than 60
seconds, send them a kill signal, and report the reaping via syslog.

Syslog log messages will be generated like the following:

    kill - PID: 27744 Srv: 13-2 Acc: 0/22/52325 M: W CPU: 7.92 Ss: 0:
    Req: 0 Conn: 0.0 Child: 0.08 Slot: 568.37 Client: 10.13.1.15 VHost:
    foo.bar.baz POST /slow.php CWD: /var/www

To run this via cron, I would suggess adding an entry like the following
to instruct cron to run it every minute:

    * * * * * /usr/local/bin/long-httpd-killer -t 60 -s


## Feedback

Please send feedback or patches through github:
https://github.com/tdsullivan/long-httpd-killer