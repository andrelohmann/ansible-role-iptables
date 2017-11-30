iptables
==========

[![Build Status](https://travis-ci.org/andrelohmann/ansible-role-iptables.svg?branch=master)](https://travis-ci.org/andrelohmann/ansible-role-iptables)

Use this role to install and manage icoming iptables rules in an easy way.

The default setting will block all incoming requests except ssh (secured by fail2ban).

Role Variables
--------------

Create a list all chains, which should allow access to the host.


    iptables:
      router: False  # True if forwarding needs to be allowed
      pingables:  # hosts, that are allowed to ping the target
      - host: monitoring_host
        ip: X.X.X.X
      custom_pre_rules: [] # add custom rules
      chains:
      - name: HTTP
        comment: "all HTTP and HTTPS Traffic"
        protocol: tcp  # tcp/icmp/udp
        ports:
        - 80
        - 443
      - name: MYSQL
        comment: "all Mysql Traffic"
        protocol: tcp # tcp/icmp/udp
        ports:
        - 3306
        sources:
        - host: mysql_read_slave
          ip: X.X.X.X
      custom_post_rules: []

Requirements
------------

This role requires debian or ubuntu.

Example Playbook
----------------

    - hosts: all
      roles:
         - { role: andrelohmann.iptables }

License
-------

MIT

Author Information
------------------

https://github.com/andrelohmann
