# Ansible Role: ssmtp

An ansible role to install and configure ssmtp

## Requirements

> This role has been tested on `Ubuntu 16.04` and `Ubuntu 16.10` only.

## Variables

- `ssmtp_smtp_server` - smtp server
  - **Required**
- `ssmtp_smtp_port` - smtp port
  - Default: `25`
- `ssmtp_use_tls` - use tls
  - Default: `no`
- `ssmtp_use_starttls` - use starttls
  - Default: `no`

- `ssmtp_auth_user` - authentication user
  - **Required**
- `ssmtp_auth_password` - authentication password
  - **Required**
- `ssmtp_auth_method` - authentication method
  - Default: `LOGIN`

- `ssmtp_sender_domain` - domain name of your sender addresses. e.g. gmail.com, company.tld.
  - **Required**
  > **Note**: some smtp servers will reject emails if this domain is unknown e.g. mandrill.

- `ssmtp_default_recipient` - address to redirect all emails sent to service accounts to. e.g. root. leave blank to disable.
  - Default: `''`

- `ssmtp_host_fqdn` - server hostname.
  - Default: `'{{ ansible_fqdn }}`
  > **Note**: must be a fully qualified domain name or some smtp servers will reject the connection e.g. gmail.

- `ssmtp_allow_sender_override` - if the 'From' header is set, it can be used.
  - Default: `yes`

- `ssmtp_sender_aliases` - list of local accounts and their sending alias
  - Default: `[]`
  - Example
    ```yaml
    ssmtp_sender_aliases:
      - name: root
        alias: aliased@company.tld
      - name: admin
        alias: admin.server2@company.tld
    ```

## Usage Example

```yaml
- hosts: all
  vars:
    ssmtp_smtp_server: smtp.gmail.com
    ssmtp_smtp_port: 587
    ssmtp_use_tls: yes
    ssmtp_use_starttls: yes
    ssmtp_auth_user: username
    ssmtp_auth_password: password
    ssmtp_sender_domain: gmail.com
    ssmtp_default_recipient: username@gmail.com
    ssmtp_allow_sender_override: no
    ssmtp_sender_aliases:
      - name: root
        alias: 'root.{{ ansible_fqdn }}@company.tld'
  roles:
    - ssmtp
```



## License

MIT / BSD

## Author Information

This role was created by [TheDumbTechGuy](https://github.com/thedumbtechguy) ( [twitter](https://twitter.com/frostymarvelous) | [blog](https://thedumbtechguy.blogspot.com) | [galaxy](https://galaxy.ansible.com/thedumbtechguy/) )

## Credits