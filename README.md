# check_pureflex_cmm
nagios check for IBM Pureflex chassis health

This script will monitor the status of the Pureflex Chassis Management Module (CMM) over SNMP.

# Requirements
You will need to enable SNMP on the CMM.  Login to the CMM web interface, click Mgt Module Management, Network, SNMP, Enable SNMP v1, set community name

# Usage
Add the following section to services.cfg on the nagios server
```
define service{
        use                             generic-24x7-service
        host_name                       cmm1
        service_description             Chassis health
        check_command                   check_cmm!public
        }
```

Add the following section to commands.cfg on the nagios server
```
# ---------------------------------------------------------------------------
# 'check_cmm' command definition
define command{
        command_name    check_cmm
        command_line    $USER1$/check_cmm -H $HOSTADDRESS$ -c $ARG1$
        }
```

Copy the `check_pureflex_cmm` file to `/usr/local/nagios/libexec/` (or wherever your distro keeps nagios checks)

