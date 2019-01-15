# ansible-ssmtp

Ansible role to setup SSMTP to forward to a remote SMTP server and configure a systemd unit which can be used to send an email when a service fails.

## Variables

The following variables can be provided to this role to customise elements of the SSMTP configuration.

| Name                                  | Default                   | Purpose                                                                                                       |
|---------------------------------------|---------------------------|---------------------------------------------------------------------------------------------------------------|
| ssmtp_root                            | postmaster                | The user that gets all mail for userids less than 1000. If blank, address rewriting is disabled.              |
| ssmtp_mailhub                         | mail                      | The SMTP server to send mail to.                                                                              |
| ssmtp_rewrite_domain                  | `{{ ansible_domain }}`    | The domain from which mail seems to come.                                                                     |
| ssmtp_hostname                        | `{{ ansible_hostname }}`  | The full qualified name of the host. If not specified, the host is queried for its hostname.                  |
| ssmtp_from_line_override              | NO                        | Specifies whether the From header of an email, if any, may override the default domain.                       |
| ssmtp_auth_user                       |                           | The username to authenticate to the SMTP server with.                                                         |
| ssmtp_auth_pass                       |                           | The password to authenticate to the SMTP server with.                                                         |
| ssmtp_auth_method                     | LOGIN                     | The authentication method to use with the SMTP server.                                                        |
| ssmtp_use_tls                         | true                      | Use TLS to connect to the SMTP server.                                                                        |
| ssmtp_use_starttls                    | true                      | Use STARTTLS to connect to the SMTP server.                                                                   |
| ssmtp_revaliases                      | []                        | An array of the form {'local_account': '', 'outgoing_address': ''} to specify aliases for local usernames.    |
| ssmtp_systemd_notification_address    | abc@gmail.com             | The email to send systemd failure notifications to.                                                            |

## Example Playbook

```
- hosts: all
  roles:
    - { role: joelnb.ansible_ssmtp }
```

## Contributors

- [Kevin Brebanov](https://github.com/kbrebanov) (Original Author - see [kbrebanov/ansible-ssmtp](https://github.com/kbrebanov/ansible-ssmtp))
- [Joel Noyce Barnham](https://github.com/joelnb) (Current Maintainer)
- [Erik Westrup](https://github.com/erikw) (The systemd email functionality is based on his repo [erikw/restic-systemd-automatic-backup](https://github.com/erikw/restic-systemd-automatic-backup))
