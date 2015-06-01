ssmtp
=====

Installs and configures sSMTP

Requirements
------------

This role requires Ansible 1.4 or higher.

Role Variables
--------------

| Name                     | Default                  | Description                                                                                     |
|--------------------------|--------------------------|-------------------------------------------------------------------------------------------------|
| ssmtp_root               | postmaster               | The person who gets all mail for userids < 1000. Make this empty to disable rewriting.          |
| ssmtp_mailhub            | mail                     | The place where the mail goes. The actual machine name is required no MX records are consulted. |
| ssmtp_rewrite_domain     | "{{ ansible_domain }}"   | Where will the mail seem to come from?                                                          |
| ssmtp_hostname           | "{{ ansible_hostname }}" | The full hostname                                                                               |
| ssmtp_from_live_override | 'NO'                     | Are users allowed to set their own From: address? ('YES' or 'NO')                               |
| ssmtp_revaliases         | []                       | Array of hashes containing reverse aliases information                                          |

Dependencies
------------

None

Example Playbook
----------------

Install sSMTP
```
- hosts: all
  roles:
    - { role: kbrebanov.ssmtp }
```

Install sSMTP specifying a mailhub
```
- hosts: all
  roles:
    - { role: kbrebanov.ssmtp, ssmtp_mailhub: mail.example.com }
```

Install sSMTP specifying reverse alias
```
- hosts: all
  vars:
    ssmtp_revaliases:
      - local_account: root
        outgoing_address: your_login@your.domain
        mailhub: mailhub.your.domain
        port: 25
  roles:
    - kbrebanov.ssmtp
```

License
-------

BSD

Author Information
------------------

Kevin Brebanov
