auditd
=========

Role for install and configure audit system. Compatable with RedHat/CentOS version 7.x only.

How to configure rules
------------

There are two ways how you can prodive rules configuration:
1. There is list `auditd_local_rules` which should contain "raw" rules, for example:
```
auditd_local_rules:
  - '-w /etc/hosts -p wa -k network_modifications'
  - '-a always,exit -F arch=b32 -S sethostname -S setdomainname -k network_modifications'
  - '-a always,exit -F arch=b64 -S sethostname -S setdomainname -k network_modifications'
```
2. There are set of pre-defined rules given by the role (most of these rules are from `/usr/share/doc/audit-<version>/rules`), list of these rules (files) should be provided through `auditd_rules_templates` array, for example:
```
auditd_rules_templates:
  - 20-dont-audit.rules
  - 30-nispom.rules
  - 71-networking.rules
```


Role Variables
--------------

`auditd_enabled`: control is `auditd` enabled or disabled (in this case package is not deleted, only service stopped and disabled);

`auditd_strict_rules_management`: if these set to `true` all unknown files in `/etc/audit/rules.d` will be deleted.

Tests
------------

There is vagrant based tests configuration if you want execute tests locally. All tests can be run by `molecule/vagrant/run` command.
