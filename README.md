Mokey
=========

Ansible role to Install Mokey

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

The role allows installing `mokey` in two ways and is configurable by setting `mokey_install_method` variable.

* `rpm` - When the method is `rpm`, `mokey_rpm_url` should be set to a valid URL reachable from the mokey host.
* `yum` - When the method is `yum`, `mokey_version` should be set, and the mokey repository should be configured on the host (`/etc/yum.repos.d`)

* Install variables

  ```
  mokey_install_method: rpm
  mokey_rpm_url: https://github.com/ubccr/mokey/releases/download/v0.0.6/mokey-0.0.6-14.el7.centos.x86_64.rpm

  mokey_version: 0.0.6
  ```

* Database configuration variables

  ```
  mokey_db_name: mokey
  mokey_db_host: localhost
  mokey_db_port: 3306
  mokey_db_user: mokey
  mokey_db_pass:
  ```

* IPA configuration variables

  ```
  mokey_keytab_dir: /etc/mokey/keytab

  mokey_ipa_adminuser:
  mokey_ipa_adminpass:
  mokey_ipa_host: ipa.example.com
  mokey_ipa_port: 443

  mokey_ipa_role_name: 'Mokey User Manager'
  mokey_ipa_role_desc: 'Mokey User management'
  mokey_ipa_role_priv: 'Modify users and Reset passwords'
  mokey_ipa_user_name: mokeyapp
  mokey_ipa_user_firstname: Mokey
  mokey_ipa_user_lastname: App
  ```

* Mokey configuration file (`mokey.yaml`) variables

 All the variables starting with `mokey_config_` will be used to template mokey configuration (`mokey.yaml`).

  ```
  mokey_config_dsn: "user:pass@/dbname?parseTime=true"
  # DSN could be configured with the available db parameters passed to the role. Eg:
  # mokey_config_dsn: "{{ mokey_db_user }}:{{ mokey_db_pass }}@tcp({{ mokey_db_host }}:{{ mokey_db_port }})/{{ mokey_db_name }}?parseTime=true"
  mokey_config_driver: mysql

  # Redirect configuration options
  mokey_config_insecure_redirect_port:
  mokey_config_insecure_redirect_host:

  # Webserver configuration options
  mokey_config_bind: "127.0.0.1"
  mokey_config_port: 8080
  mokey_config_cert:
  mokey_config_key:
  mokey_config_min_passwd_len:
  mokey_config_auth_key: mysecret
  mokey_config_enc_key: mysecret

  # 2FA configuration options
  mokey_config_force_2fa: "true"
  mokey_config_require_question_pwreset: "true"

  # IPA configuration options
  mokey_config_ipahost:
  mokey_config_keytab: "/path/to/client.keytab"

  # Redis configuration options
  mokey_config_rate_limit: "false"
  mokey_config_redis:
  mokey_config_max_requests:
  mokey_config_rate_limit_expire:

  # Email configuration options
  mokey_config_smtp_host: localhost
  mokey_config_smtp_port: 25
  mokey_config_email_from: "helpdesk@example.edu"
  mokey_config_email_sig: "Mr. System Administrator"
  mokey_config_email_link_base: "http://localhost:8080"
  mokey_config_email_prefix: "mokey"
  mokey_config_setup_max_age: 86400
  mokey_config_reset_max_age: 3600
  mokey_config_max_attempts: 10
  mokey_config_pgp_sign: "false"
  mokey_config_pgp_key:
  mokey_config_pgp_passphrase:

  mokey_config_develop: "false"
  ```

Dependencies
------------

This role expects a running version IPA that is compatible with the version of `mokey`.
The `mokey_db_user` and `mokey_db_pass` should be created and configured prior to running this role.

Example Playbook
----------------

    - hosts: servers
      roles:
         - role: mokey

License
-------

MIT

Author Information
------------------

Ranjandas (https://github.com/Ranjandas)
