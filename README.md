TACACS+
========

Setup a TACACS+ server using [`tac_plus`](http://www.shrubbery.net/tac_plus/) from Shrubbery Networks.

While TACACS+ supports Authentication, Authorization, and Accounting (AAA), this role is limited to configuring
authentication. When calling the role, a list of users should be passed in (along with PAP or ascii passwords for each user). 
This information is used to generate a ['tac_plus' configuration file](templates/etc-tac_plus.conf.j2).

Requirements
------------

* EL 7
* Port 49 (TCP)

Role Variables
--------------

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `tacacs_secret_key` | `CHANGEME` | Secret key shared between client and `tac_plus` server | 
| `tacacs_users` | `(empty)` | Set of users to be authenticated by the `tac_plus` server (see example below). |


Example Playbook
-------------------------

When calling the `tacacs` role, a list of users should be provided. Each user should be assigned either
`pap_password`, `ascii_password`, or both.

Note: The role will not actually create user accounts on the target host. They will only be defined in the 
['tac_plus' configuration file](templates/etc-tac_plus.conf.j2).

```
---
- hosts: tacacs
  roles:
     - role: jladdjr.tacacs_plus
       tacacs_users:
          - username: alice
            pap_password: alice_pap
            ascii_password: alice_ascii
          - username: bill
            pap_password: bill_pap
          - username: chris
            ascii_password: chris_ascii
```

License
-------

MIT
