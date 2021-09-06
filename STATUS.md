PROGRESS:
* Finished:
  - ./tasks/main.yml
  - ./tasks/check_prereqs.yml
  - ./tasks/prelim.yml
  - ./tasks/parse_etc_password.yml
  - ./tasks/section_1/main.yml
  - ./tasks/section_1/cis_1.1.x.yml
  - ./tasks/section_1/cis_1.1.1.x.yml
  - ./tasks/section_1/cis_1.2.x.yml
  - ./tasks/section_1/cis_1.3.x.yml
  - ./tasks/section_1/cis_1.4.x.yml
  - ./tasks/section_1/cis_1.5.x.yml
  - ./tasks/section_1/cis_1.6.x.yml
  - ./tasks/section_1/cis_1.7.x.yml
  - ./tasks/section_1/cis_1.8.x.yml
  - ./tasks/section_2/main.yml
  - ./tasks/section_2/cis_2.1.x.yml
  - ./tasks/section_2/cis_2.1.1.x.yml
  - ./tasks/section_2/cis_2.2.x.yml
  - ./tasks/section_2/cis_2.3.x.yml
  - ./tasks/section_3/main.yml
  - ./tasks/section_3/cis_3.1.x.yml
  - ./tasks/section_3/cis_3.2.x.yml
  - ./tasks/section_3/cis_3.3.x.yml
  - ./tasks/section_3/cis_3.4.x.yml
  - ./tasks/section_3/cis_3.5.1.x.yml
  - ./tasks/section_3/cis_3.5.2.x.yml
  - ./tasks/section_3/cis_3.5.3.1.x.yml
  - ./tasks/section_4/main.yml
  - ./tasks/section_4/cis_4.1.1.x.yml
  - ./tasks/section_4/cis_4.1.2.x.yml
  - ./tasks/section_4/cis_4.1.x.yml
  - ./tasks/section_4/cis_4.2.x.yml
  - ./tasks/section_4/cis_4.2.2.x.yml
  - ./tasks/section_5/main.yml
  - ./tasks/section_5/cis_5.1.x.yml
  - ./tasks/section_5/cis_5.2.x.yml
  - ./tasks/section_5/cis_5.3.x.yml
  - ./tasks/section_5/cis_5.4.x.yml
  - ./tasks/section_5/cis_5.5.1.x.yml
  - ./tasks/section_5/cis_5.5.x.yml
  - ./tasks/section_5/cis_5.7.x.yml
  - ./tasks/section_5/cis_5.7.x.yml
  - ./tasks/section_6/main.yml
  - ./tasks/section_5/cis_6.1.x.yml
  - ./tasks/section_5/cis_6.2.x.yml
  - ./tasks/post.yml

* Skipping (for now):
  - ./tasks/pre_LI_audit.yml
  - ./tasks/section_3/cis_3.5.3.x.yml
  - ./tasks/section_3/cis_3.5.3.2.yml
  - ./tasks/section_3/cis_3.5.3.3.yml
  - ./tasks/post_LE_audit.yml

* Started:
  -

GO BACK AND CHECK:
* ./tasks/main.yml: lines 85 - 101
  - Not sure if this is the correct Task number
  -
* ./tasks/parse_etc_password.yml; the variable "amznlnx2cis_passwd_tasks" is not defined anywhere (what's it for?)
* 4.1.1.3 - There is no GRUB_CMDLINE_LINUX by default, but there is a GRUB_CMDLINE_LINUX_DEFAULT.  Should that be included?
* 3.5.1.5 - FAILING if you run the playbook a 2nd time

Prerequisites before running the playbook:
* 1.1.10 - Ensure separate partition exists for /var
  - Recommend adding a separate partition to the AMI
* 1.1.11 - Ensure spearate partition exists for /var/tmp
  - Recommend adding a separate partition to the AMI
* 1.1.15 - Ensure separate partition exists for /var/log
  - Recommend adding a separate partition to the AMI
* 1.1.16 - Ensure separate partition exists for /var/log/audit
  - Recommend adding a separate partition to the AMI
* 1.1.17 - Ensure separate partition exists for /home
  - Recommend adding a separate partition to the AMI
* 1.7.1.1 - Ensure message of the day is configured properly
  - Modify the variable 'amznlnx2cis_warning_banner' to define the message of the day (i.e. logon message)
* 1.7.1.2 - Ensure local login warning banner is configured properly
  - Modify the variable 'amznlnx2cis_warning_banner' define the login warning banner
* 1.8 - Ensure updates, patches, and additional security software are installed
  - Default setting will run a yum update. To change this, modify the 'amznlnx2cis_rule_1_8' to false
* 2.1 - Special Purpose Services
  - Review the list of services and make sure none are required (default is to UNINSTALL)
* 2.1.1 - Time Synchronization
  - amznlnx2cis_time_synchronization - Specify what the preferred NTP utility to use (chrony or ntp)
  - Variable: 'amznlnx2cis_time_synchronization_servers' - Specify the NTP servers
* 3.1.1 - Disable IPv6
  - Default setting is that IPv6 IS required
  - Change the variable 'amznlnx2cis_ipv6_required' to false if it is NOT needed
* 3.5 - Firewall
  - Select the desired firewall application via the variable 'amznlnx2cis_firewall'
  - Default setting is: firewalld
* 4.1.2.3 - Ensure system is disabled when audit logs are full
  - If the system should not be halted when audit logs are full, then change the variable 'admin_space_left_action'
  - Halt is normally for 'high security contexts'
  - Valid values are ignore, syslog, email, suspend, single, and halt
* 4.2.1.1 - Ensure rsyslog is installed
  - The default logger is rsyslog.  If syslog-ng is prefered, the 'amznlnx2_syslog' variable must be changed
* 4.2.1.5 - Ensure rsyslog is configured to send logs to a remote log host
  - Need to change the variable 'amznlnx2cis_remote_log_server' to point to the log host
* 5.3.4 - Ensure SSH access is limited
  - This control limits users/groups ability to log into ssh.  It's "recommended" one of the following four variables should be configured to be compliant.  The default is none of these are configured.
    - allowusers
    - allowgroups
    - denyusers
    - denygroups
* 5.3.16 - Ensure SSH Idle Timeout Interval is configured
  - Modify the variable 'clientaliveinterval' to change the default timeout of 15 minutes (can't be higher than 900 seconds)
* 5.7 - Ensure access to the su command is restricted
  - Uncomment and modify the variable 'amznlnx2cis_sugroup' with the group name that should have permissions to run su
  - Otherwise by default, only the 'root' account will have this permission
